# Automatic Reference Counting

[Automatic Reference Counting - The Swift Programming Language (Swift 5.1)](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html)

Swift는 앱의 메모리 사용을 추적하고 관리 하기 위해 Automatic Reference Counting (ARC)를 사용합니다. 대부분의 경우, 이것은 Swift에서 메모리 관리를 "그냥 작동된다"는 것을 의미하고, 당신이 메모리 관리에 대해서 생각 할 필요가 없습니다. 클래스 인스턴스에 의해 사용 되는 메모리가 더이상 필요 하지 않을 때 ARC는 메모리를 해제합니다.

하지만, 몇몇 케이스에서 ARC는 메모리를 관리 하기 위해 당신의 코드의 부분 간의 관계에 대한 더 많은 정보를 요구합니다. 이번 챕터에서는 그러한 상황들에 대해 설명하고 ARC가 당신의 앱의 모든 메모리를 관리할 수 있도록 하는지 보여줄 겁니다. Swift에서 ARC를 사용하는 것은 Obective-C로 ARC를 사용하는 Transitioning to ARC Release Notes에서의 설명과 매우 유사합니다.

Reference counting은 클래스의 인스턴스에서만 적용 가능합니다. 구조체나 열거형은 참조 타입이 아닌, 값 타입이고 레퍼런스에 의해 저장되고 전달 되지 않습니다.

