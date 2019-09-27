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

다음 코드는 `Person` 인스턴스를 생성하기 위해 사용 되는 다수의 참조를  `Person?` 타입의 3개의 변수를 정의하고 있습니다. 이 변수들이 옵셔널 타입이기 때문에(`Person`이 아닌,`Person?`), 자동으로 `nil` 값으로 초기화 되고, 현재는 `Person` 인스턴스를 참조하고 있지 않습니다.

```swift
    var reference1: Person?
    var reference2: Person?
    var reference3: Person?
```

이제 새로운 `Person` 인스턴스를 초기화하고 3개 변수들 중 하나를 할당 할 수 있습니다.

```swift
    refernce1 = Person(name: "Jinha Park")
    // Prints "Jinha Park is being initialized"
```

`Person`클래스의 생성자를 호출하는 시점에 "Jinha Park is being initialized" 라는 메세지가 출력되는 것을 주목하세요. 이것은 초기화가 이루어졌다는 것을 확인해 줍니다.

`Person`인스턴스가 `reference1` 변수에 할당이 되었기 때문에, `reference1`에서 `Person`인스턴스에 강한 참조가 되고 있습니다. 적어도 하나의 강한 참조가 있기 때문에, ARC는 `Person`을 메모리에 유지 시키도록 할 것이고 해제되지 않습니다.

같은 `Person`인스턴스를 두 개의 변수에 더 할당하면, 인스턴스에 두개의 강한 참조가 생기게 됩니다.

```swift
    refernce2 = refernce1
    refernce3 = refernce1
```

여기엔 하나의 `Person` 인스턴스에 세개의 강한 참조가 있습니다.

만약 이 두개의 강한 참조(기존 참조를 포함한)를 두개의 변수에 nil을 할당으로서 깨고 싶다면, 하나의 강한 참조는 남아있고, `Person`인스턴스는 해제되지 않을 것입니다.

```swift
    refernce1 = nil
    refernce2 = nil
```

ARC는 세번째 그리고 마지막 강한 참조가 깨지기 전까지, `Person`인스턴스를 해제하지 않습니다. `Person` 인스턴스를 더이상 사용 하지 않는 시점에 해제 됩니다.

```swift
    refernce3 = nil
    // Prints "Jinha Park is being deinitialized"
```

## 클래스 인스턴스 간 강한 순환 참조 (Strong Reference Cycles Between Class Instances)

위의 예제에서, ARC는 생성한 새로운 `Person` 인스턴스의 참조의 개수를 추적 할 수 있고 `Person` 인스턴스가 더이상 필요 없을 때 해제 할 수 있습니다.

하지만, 클래스의 인스턴스의 강한 참조가 0 이 되는 시점이 전혀 생기지 않는 코드를 작성하게 될 수도 있습니다. 이것은 두 개의 클래스 인스턴스가 서로 강한 참조를 하고, 각각의 인스턴스가 다른 인스턴스를 살려 둘 경우에 발생할 수 있습니다. 이것은 강한 참조 순환이라고 알려져 있습니다.

클래스 간의 관계를 strong 참조 대신 weak 또는 unowned 참조로 정의 함으로써 강한 순환 참조를 해결 할 수 있습니다. 이 과정은 클래스 인스턴스 간의 강한 순환 참조 해결하기(Resolving Strong Refernce Cycles Between Class Instances)에서 설명되어 있습니다. 하지만, 강한 참조 순환의 해결 방법을 배우기 전에, 강한 순환 참조가 어떻게 발생 하는지에 대해 이해하는 것이 도움이 될 것 입니다.

여기 강한 순환 참조가 어떻게 우연히 생기는 지에 대한 예시가 있습니다. 이 예시는  아파트의 단지와 거주자의 모델화한 `Person`과 `Apartment`라는 클래스를 정의 하고 있습니다.

```swift
    class Person {
    	let name: String
    	
    	init(name: String) { self.name = name }
    
    	var apartment: Apartment?
    
    	deinit { print("\(name) is being deinitialized") }
    }
    
    class Apartment {
    	let unit: String
    	
    	init(unit: String) { self.unit = unit }
    
    	var tenant: Person?
    
    	deinit { print("Apartment \(unit) is being deinitialized") }
    }
```

모든 `Person` 인스턴스는 `String` 차입의 `name` 프로퍼티와 `nil`로 초기화 된 옵셔널 타입의 `apartment`프로퍼티를 가지고 있습니다. 사람이 항상 아파트를 가지고 있지 않기 때문에 `apartment` 프로퍼티는 옵셔널입니다.

유사하게, 모든 `Apartment`는 `String`타입의 `unit`과 `nil`로 초기화 된 옵셔널 타입 `tenant`을 가지고 있습니다. 아파트에 항상 세입자가  있는 것이 아니기 때문에 세입자 프로퍼티는 옵셔널 입니다.
