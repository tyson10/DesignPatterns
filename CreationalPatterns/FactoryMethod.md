# Factory Method

- 개념
    - 부모 클래스에 알려지지 않은 구체적인 클래스를 생성하는 패턴이며, 자식 클래스가 어떤 객체를 생성할지 결정하는 패턴.
- 구조
    - Creator: Factory의 기본을 정의하는 객체.
    - Concrete Creator:  Creator를 채택하고 있으며, product에 따른 구체적 기능을 구현하는 객체.
    - Product: Concrete Product가 수행해야할 동작을 선언하는 객체.
    - Concrete Product: Product를 채택하며 그에 맞게 만든 실제 객체.
- 장점
    - 프로토콜로 기본 기능을 정의해 주었기 때문에, 프로토콜만 준수하도록 구현한다면 새로운 클래스를 추가하기 쉬움.
    - 코드에 수정사항이 생기더라도 팩토리 메소드만 수정하면 되므로 수정이 쉬움.
    - 단일 책임 원칙
    - 개방/폐쇄 원칙
- 단점
    - product가 추가될 때 마다 새로운 클래스를 작성해야 하므로 클래스가 많아지고, 복잡도가 증가할 수 있음.

예시

```swift
// Creator
protocol AppleFactory {
    func createElectronics() -> Product
}

// Concrete Creator
class IPhoneFactory: AppleFactory {
    func createElectronics() -> Product {
        return IPhone()
    }
}

class IPadFactory: AppleFactory {
    func createElectronics() -> Product {
        return IPad()
    }
}

// Product
protocol Product {
    func produceProduct()
}

// Concrete Product
class IPhone: Product {
    func produceProduct() {
        print("Hello, iPhone was made")
    }
}

class IPad: Product {
    func produceProduct() {
        print("Hello, iPad wad made")
    }
}

// 팩토리 메소드를 사용하는 코드를 보통 클라이언트 코드라고 부른다.
class Client {
    func order(factory: AppleFactory) {
        let elctronicsProduct = factory.createElectronics()
        elctronicsProduct.produceProduct()
    }
}

var client = Client()

client.order(factory: IPadFactory())
client.order(factory: IPhoneFactory())

/*
Hello, iPad was made
Hello, iPhone was made
*/
```
