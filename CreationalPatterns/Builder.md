# Builder

- 개념
    - 복잡한 객체를 생성하기에 유용한 패턴.
- 구조
    - Product와 Builder로 구성됨.
    - Builder 는 어떤 값들을 세팅하는 메소드와 최종적으로 product를 만드는 build() 메소드를 가짐.
- 언제 사용할까?
    - Swift에서는 초기화 함수랑 프로퍼티 기본값을 통해서 더 간단히 구현할 수 있기는 함.
    - 생성해야할 객체의 프로퍼티 갯수가 아주 많거나, 복잡해지는 경우 사용하면 유용할 수 있음.

예시

```swift
struct Phone {
    let color: String
    let storage: String
}

class PhoneBuilder {
    private var color = "Space Gray"
    private var storage = "256GB"

    func setColor(_ color: String) -> MacBookBuilder {
        self.color = color
        return self
    }

    func setStorage(_ storage: String) -> MacBookBuilder {
        self.storage = storage
        return self
    }

    func build() -> MacBook {
        return MacBook(color: color, storage: storage)
    }
}

let builder = PhoneBuilder()
let phone1 = builder.setColor("Silver").setStorage("512").build()
let phone2 = builder.setStorage("1TB").build()
let phone3 = builder.build()
```
