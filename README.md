# DDD (Domain Driven Design)

- [Domain](#domain)
- [Architecture](#architecture)
- [Aggregate](#aggregate)
- [Repository](#repository)
- [Domain Service](#domain-service)
- [Inner Class](#inner-class)
  
## Domain
- 구현해야 할 소프트웨어 대상
- 소프트웨어로 해결해결하고자 하는 문제 영역
- `하나의 도메인`은 다쉬 `하위 도메인`으로 나눌 수 있다
- 도메인에 대한 이해 없이 코딩을 시작할 수 없다
  
###### domain model
- 도메인 자체를 이해하기 위한 `개념 모델`
- 특정 도메인을 개념적으로 표현한 것 `(ex: as Object, as Diagram)`
- 여러 관계자들이 동일한 모습으로 도메인을 이해하고 도메인 지식을 공유하는 데 도움이 된다
  - `개념 모델` : 순수하게 문제를 분석한 결과물
  - `구현 모델` : 개념 모델을 구현 가능한 형태의 모델로 전환한 것  
- 도메인에 대한 `핵심 구성요소`, `규칙`, `기능`
- `get/set` 메서드를 무조건 추가하는 것은 좋지 않은 습관이다
- 특히 `set` 메서드는 도메인의 핵심 개념이나 의도를 코드에서 사라지게 한다
- 도메인의 필드에서 각각 set 메서드를 사용하는 것은 데이터를 누락할 수 있는 여지를 남겨두기 때문에
- 객체 생성시점에 필요한 값들을 전부 매개변수를 전달하는 것이 적합하다

###### entity
- 식별자 : 엔티티 객체마다 고유의 식별자를 갖는다
```java
public class Order {
  // 상품을 주문할 때 사용하는 주문번호는 서로 중복될 수 없는 고유한 값이여야 한다
  private String orderNumber;
}
```
  
###### value
- 밸류 타입 : 개념적으로 완전한 하나를 표현할 때 사용
```java
// name, phoneNumber 필드들을 개념상 하나로 묶을 수 있기 때문에
// Receiver 라는 밸류타입 내부에서 그룹화하여 정의한다

public class Receiver {
  private String name;
  private String phoneNumber;
  (...)
}

// 주소도 필요한 항목들도 마찬가지로 밸류타입으로 그룹화 할 수 있다
public class Address {
  private String address1;
  private String address2;
  private String zipCode;
  (...)
}
```
- 밸류 타입을 위한 기능을 추가할 수도 있다
- 밸류 객체의 데이터를 변경할 때는 새로운 밸류 객체를 생성하는 방식이 적합하다
- 데이터 변경기능 제공하지 않는 이유는 보다 안전한 코드 작성을 위함이다
```java
pulibc Class Money {
  private int value;
  
  public Money add(Money money) {
    return new Money(this.value + money.value);
  }
  
  public Money multiply(int multiplier) {
    return new Money(value * multiplier);
  }
}
```
  
## Architecture
- 계층 구조 : 표현 > 응용 > 도메인 > 인프라스트럭처
- 고수준 모듈 : 의미 있는 단일 기능을 제공하는 모듈 `ex) 응용, 도메인 영역`
- 저수준 모듈 : 하위 기능을 실제로 구현한 것 `ex) 인프라스트럭처`
- DIP(Dependency Inversion Principle) 의존 역전 원칙 : 저수준 모듈이 고수준 모듈을 의존
  
  
  
## Aggregate
## Repository
## Domain Service
## Inner Class
## [Ref.]
  - https://jhkang-tech.tistory.com/48
  - https://javacan.tistory.com/entry/what-is-a-domain-model
  - https://medium.com/react-native-seoul/%EB%8F%84%EB%A9%94%EC%9D%B8-%EC%A3%BC%EB%8F%84-%EC%84%A4%EA%B3%84-domain-driven-design-in-real-project-1-%EB%8F%84%EB%A9%94%EC%9D%B8-83a5e31c5e45
