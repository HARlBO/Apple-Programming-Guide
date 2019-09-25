# Automatic Reference Counting

[Automatic Reference Counting - The Swift Programming Language (Swift 5.1)](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html)

Swift는 앱의 메모리 사용을 추적하고 관리 하기 위해 Automatic Reference Counting (ARC)를 사용합니다. 대부분의 경우, 이것은 Swift에서 메모리 관리를 "그냥 작동된다"는 것을 의미하고, 당신이 메모리 관리에 대해서 생각 할 필요가 없습니다. 클래스 인스턴스에 의해 사용 되는 메모리가 더이상 필요 하지 않을 때 ARC는 메모리를 해제합니다.

하지만, 몇몇 케이스에서 ARC는 메모리를 관리 하기 위해 당신의 코드의 부분 간의 관계에 대한 더 많은 정보를 요구합니다. 이번 챕터에서는 그러한 상황들에 대해 설명하고 ARC가 당신의 앱의 모든 메모리를 관리할 수 있도록 하는지 보여줄 겁니다. Swift에서 ARC를 사용하는 것은 Obective-C로 ARC를 사용하는 Transitioning to ARC Release Notes에서의 설명과 매우 유사합니다.

Reference counting은 클래스의 인스턴스에서만 적용 가능합니다. 구조체나 열거형은 참조 타입이 아닌, 값 타입이고 레퍼런스에 의해 저장되고 전달 되지 않습니다.

## ARC의 동작 방식(How ARC Works)

클래스의 새 인스턴스를 생성 할 때 마다, ARC는 인스턴스에 대한 정보를 저장 하기 위해 메모리의 덩어리를 할당합니다. 이 메모리는 인스턴스의 타입에 대한 정보와 그 인스턴스와 관련된 저장 프로퍼티의 값도 가지고 있습니다.

추가적으로, 인스턴스가 더이상 필요 없어지면, ARC는 메모리가 다른 목적으로 사용 되어 질 수 있도록 그 인스턴스에 의해 사용 된 메모리를 해제합니다. 이것은 클래스 인스턴스가 그들이 더이상 필요 없을 때 메모리의 공간을 차지 하고 있지 않다는 것을 보장합니다.

하지만, ARC가 여전히 사용 되고 있는 인스턴스를 해제 했다면, 인스턴스 프로퍼티에 더이상 접근 할 수 없거나, 인스턴스의 메소들를 호출 할 수 없습니다. 만약 인스턴스에 접근 하려 한다면, 앱은 대부분 아마도 크래시가 날 것 입니다.

인스턴스가 사용 되는 동안에 사라지지 않게 하기 위해서는, ARC는 얼마나 많은 프로퍼티, 상수, 그리고 변수들이 현재 각각의 클래스 인스턴스에 참조되고 있는지 추적합니다. ARC는 존재하는 인스턴스에 적어도 하나의 활성화된 레퍼런스가 있다면 인스턴스르 해제하지 않을 것 입니다.

클래스 인스턴스를 프로퍼티, 상수 혹은 변수에 할당 할 때 언제든지, 프로퍼티, 상수, 변수는 이것을 가능하게 하기 위해 인스턴스에 강한 참조를 만듭니다. 이 참조는 강한 참조로 불립니다. 왜냐하면 그 인스턴스에 단단한 고정을 유지하고, 강한 참조가 남아 있는 한 해제를 허용하지 않습니다.

## ARC의 사용(ARC in Action)

여기 Auto Reference Counting의 동작 방식에 대한 예제가 있습니다. 이 예제는 `name`이라는 저장 상수 프로퍼티를 정의하는 `Person` 이라는 간단한 클래스로 시작합니다.

```swift
    class Person {
    	let name: String
    
    	init(name: String) {
    		self.name = name
    		print("\(name)is being initialized")
    	}
    
    	deinit {
    		print("\(name)is being deinitialized")
    	}
    }
```

 `Person` 클래스는 인스턴스의 `name` 프로퍼티를 세팅하고 초기화가 진행 중임을 나타내는 메시지를 출력 해주는 생성자를 갖고 있습니다. `Person` 클래스는 클래스의 인스턴스가 해제 될 때 메세지를 출력하는 소멸자 또한 가지고 있습니다.
