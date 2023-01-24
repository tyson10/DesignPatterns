# Prototype

- 개념
    - 기존의 객체를 복제하기 위한 패턴.
- 구조
    - 자기 자신을 복제해서 반환하는 clone 메소드를 가짐.
- 언제 사용할까?
    - 기존의 객체를 복제할 때.
    - 프로토타입 프로토콜을 준수하는 프로토타입 객체를 복사할 때, 해당 객체의 클래스를 알지 못하더라도 복제가 가능함. 즉, 클래스 의존성 낮아짐.
    - 기존 객체를 복제하는 방식이므로 생성시에 비용이 낮아질 수 있음.
    - 접근이 제한된 프로퍼티를 가진 객체를 복사하는 경우에도 유용할 듯.
    - 복잡한 객체들에 대한 사전 설정들을 처리할 때 상속 대신 사용할 수 있음.
- 단점
    - 순환 참조가 있는 복잡한 객체에 적용하는게 어려울 수 있음.

예시
```swift
protocol Prototype: AnyObject {
    func clone() -> Self
}

class Person: Prototype {
    var age: Int

    init(age: Int) {
        self.age = age
    }

    func clone() -> Self {
        return Person(age: self.age) as! Self
    }
}

let john = Person(age: 13)
john.age += 20

let harry = john.clone()
harry.age += 10
```
