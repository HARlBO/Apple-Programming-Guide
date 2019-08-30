# Increasing Performance by Reducing Dynamic Dispatch

[Increasing Performance by Reducing Dynamic Dispatch - Swift Blog](https://developer.apple.com/swift/blog/?id=27)

다른 많은 언어들 처럼, Swift는 클래스에서 superclass에 선언된 메소드와 프로퍼티를 override 할 수 있습니다. 이것은 프로그램이 런타임에 어떤 메소드나 프로퍼티가 참조 되었는지 결정해야 하고 직접 호출 또는 간접 접근을 수행해야 한다는 것을 의미합니다. 다이나믹 디스패치(dynamic dispath)로 불리는 이 기술은, 각각의 간접적 사용에 따라 거듭되는 런타임 오버헤드의 비용으로 언어의 표현성을 증가시킵니다. 성능에 민감한 코드에서 그러한 오버헤드는 바람직하지 않습니다. 이 글은 dynamism을 제거함으로써(final, private, 모듈 최적화) 성능을 향상시키는 세가지 방법을 보여줍니다. 

아래 예시를 살펴 봅시다.
```swift
    class ParticleModel {
    	var point = ( 0.0, 0.0 )
    	var velocity = 100.0
    
    	func updatePoint(newPoint: (Double, Double), newVelocity: Double) {
    		point = newPoint
    		velocity = newVelocity
    	}
    
    	func update(newP: (Double, Double), newV: Double) {
    		updatePoint(newP, newVelocity: newV)
    	}
    }
    
    var p = ParticleModel()
    for i in stride(from: 0.0, through: 360, by: 1.0) {
    	p.update((i * sin(i), i), newV:i*1000)
    }
```
작성 된 대로, 컴파일러는 동적으로 디스패치 호출 할 것입니다. 다음을 하기 위해:

1. p의 update를 호출
2. p의 updatePoint 호출
3. p의 point 튜플 프로퍼티 접근
4. p의 velocity 프로퍼티 접근

이것이 당신이 이 코드를 보고 기대한 것이 아닐 수도 있습니다.ParticleModel의 서브클래스들이 연산 프로퍼티로 point 또는 velocity를 override하거나 새로운 구현으로 updatePoint()나 update() 로 인해 동적 호출은  필요합니다.

Swift에서, 동적 디스패치 호출은 메소드 테이블에서 함수를 찾고 간접적인 호출을 수행하도록 구현되었습니다. 이것은 직접 호출을 수행하는 것보다는 느립니다. 게다가, 간접 호출은 많은 컴파일러 최적화를 방지하기 때문에, 더 많은 비용이 들게 합니다. 성능이 중요한 코드에서 성능 향상을 필요 할 때 이런 동적인 행동을 제한 할 수 있는 기술이 있습니다. 

### override 할 필요가 없는 속성 선언을 할 때 final을 사용하라

final 키워드는 클래스, 메소드 또는 프로퍼티의 선언이 override 될 수 없다는 제한을 해줍니다. 이것은 컴파일러가 간접 동적 디스패치를 안전하게 생략 할 수 있도록 해준다. 예를 들어, 아래의 point와 velocity는 객체의 저장 프로퍼티를 통해 간적접으로 접근되고 updatePoint()는 직접 함수 호출을 통해 호출 될 것입니다. 반대로, update()는 서브클래스가 커스터마이징 된 함수로 update()를 오버라이드 할 수 있도록 허용하면서 여전히 동적 디스패치를 통해 호출 됩니다.
```swift
    class ParticleModel {
    	final var point = ( x: 0.0, y: 0.0 )
    	final var velocity = 100.0
    
    	final func updatePoint(newPoint: (Double, Double), newVelocity: Double) {
    		point = newPoint
    		velocity = newVelocity
    	}
    
    	func update(newP: (Double, Double), newV: Double) {
    		updatePoint(newP, newVelocity: newV)
    	}
    }
```
클래스 자신의 final을 표기 함으로써 전체 클래스에 적용 가능합니다. 이거슨 클래스가 서브클래싱 되는것을 막고, 클래스의 모든 함수와 프로퍼티 또한 final임을 나타냅니다.
```swift
    final class ParticleModle {
    	var point = (x: 0.0, y: 0.0)
    	var velocity = 100.0
    	// ...
    }
```

### 한 파일에서 참조되는 선언에 private 키워드를 붙이면 final임을 암시한다.

private 키워드를 선언에 적용하는 것은 현재 파일에서 선언의 가시성을 제한합니다. 이것은 컴파일러가 잠재적으로 override 된 선언을 찾는 것을 가능하게 합니다. override 된 선언의 부재는 컴파일러는 자동으로 final 키워드를 추론하고 메소드와 프로퍼티 접근에 대한 간접적인 호출을 제거 합니다. 

현재 파일에서 어떤 클래스도 ParticleModel을 override 하지 않는 다고 가정하면, 컴파일러는 모든 동적 디스패치 호출을  직접 호출을 하는 private 선언 호출로 대체 할 수 있습니다.
```swift
    class ParticleModle {
    	private var point = (x: 0.0, y: 0.0)
    	private var velocity = 100.0
    
    	private func updatePoint(newPoint: (Double, Double), newVelocity: Double) {
    		point = newPoint
    		velocity = newVelocity
    	}
    	
    	func update(newP: (Double, Double), newV: Double) {
    		updatePoint(newP, newVelocity: newV)
    	}
    }
```
이전 예시에서 처럼, point와 velocity는 직접적으로 접근 되고 updatePoint() 직접 호출 된다. 또한, update()는 update()가 private이 아니기 때문에 간접적으로 호출될 것입니다.

final과 마찬가지로, 클래스 선언 자체에 private을 적용하여 클래스 자체를 private 속성으로 만들고 클래스의 모든 프로퍼티와 메소드 모두 적용됩니다.
```swift
    private class ParticleModle {
    	var point = (x: 0.0, y: 0.0)
    	var velocity = 100.0
    	// ...
    }
```
### internal 선언에 final을 추론 하기 위해 전체 모듈 최적화를 사용하라

internal 접근자가 있는 선언(아무것도 선언 되지 않았을 때 default인)은 그들이 선언 된 모듈 안에서만 가시적입니다. Swift는 보통 모듈을 구성하는 파일을 개별적으로 컴파일 하기 때문에, 컴파일러는 다른 파일에서 internal 선언이 override 되었는지 아닌지 알 수가 없습니다. 하지만, 전체 모듈 최적화가 가능하면, 모든 모듈이 동시에 같이 컴파일됩니다. 이것은 컴파일러가 모듈 전체를 추론 할 수 있고 가시적인 override가 없다면 선언부의 internal을 final로 추론 할 수 있게 합니다.

이번에는 추가적인 public 키워드가 ParticleModel에 추가된 원래 코드의 부분으로 돌아가 봅시다.
```swift
    public class ParticleModel {
    	var point = (x: 0.0, y: 0.0)
    	var velocity = 100.0
    	
    	func updatePoint(newPoint: (Double, Double), newVelocity: Double) {
    		point = newPoint
    		velocity = newVelocity
    	}
    	
    	public func update(newP: (Double, Double), newV: Double) {
    		updatePoint(newP, newVelocity: newV)
    	}
    	
    	var p = ParticleModel()
    	for i in stride(from: 0.0, through: 360, by: 1.0) {
    		p.update((i * sin(i), i), newV:i*1000)
    	}
```
전체 모듈 최적화의 부분을 컴파일 할때, 컴파일러는 point, velocity 프로퍼티 그리고 updatePoint()호출 을 통해 final을 추론 할 수 있습니다. 반대로, update()는 update()가 public 접근자를 갖고 있기 때문에 추론 될 수 없습니다.


