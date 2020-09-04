## OOP (Object Oriented Programming)
### 클래스? 오브젝트? 인스턴스?
- 클래스 : 객체를 생성하기 위해 변수와 메소드를 정의하는 일종의 틀. 객체의 **설계도**
- 오브젝트 : 클래스로 구현할 대상. **클래스를 바탕으로 나온 결과물**.
- 인스턴스 : 소프트웨어에 실체화 한 대상. **메모리를 받은 객체**. 인스턴스는 객체에 포함된다고 볼 수 있다.
- 참고자료
  - https://dongkka.tistory.com/22
  - https://cerulean85.tistory.com/149

### 상속과 다형성
- 상속 : 부모 클래스의 변수와 메서드를 물려받아서 사용하는 것. **재사용성**.
- 다형성 : 같은 모양의 코드가 다른 행위를 하는 것. 스마트폰의 키패드가 다이얼, 게임, 메신저 등 모양은 같지만 다른 기능을 하는 것에 비유할 수 있다. 오버라이딩, 오버로딩이 그 예.
- 참고자료
  - http://tcpschool.com/cpp/cpp_inheritance_derivedClass
  - https://brunch.co.kr/@kd4/4
### 자바스크립트의 Prototype, Class
- 공통점
  - OOP 에 활용할 수 있다.
  - new 키워드로 인스턴스를 생성할 수 있다.
- Class 의 특징
  - extends 키워드로 간단하게 상속을 구현할 수 있다.
  - 클래스 기반 언어에 익숙한 사람이 빠르게 학습할 수 있다.
  - 프로토타입보다 문법적으로 엄격한 편이다.
  - super 키워드로 부모 클래스의 생성자, 메서드를 호출할 수 있다.
  - 구현에 프로토타입이 사용됐다.
```javascript
  class Parent {}

  class Child extends Parent {}

  console.log(Child.__proto__ === Parent); // true
  console.log(Child.prototype.__proto__ === Parent.prototype); // true
```
- Prototype 의 특징
  - 자바스크립트의 모든 객체는 부모 역할의 객체와 연결되어 있는데, 이를 프로토타입이라고 한다.
  - 객체 생성 방식에 따라 프로토타입 객체가 다르다
    - 객체 리터럴, Object 생성자 함수 : Object.prototype
    - 생성자 함수 : 생성자_함수_이름.prototype
  - 객체의 프로퍼티를 참조할 때, 해당 객체에 없다면 **프로토타입 체인**이 동작한다.
  - 모든 객체는 [[Prototype]] 인터널 슬롯을 갖는다. 객체의 입장에서 자신의 부모 역할을 하는 프로토타입 객체를 가리키며 함수 객체의 경우 Function.prototype를 가리킨다.
  - Prototype 프로퍼티 : 함수 객체가 생성자로 사용될 때 이 함수를 통해 생성될 객체의 부모 역할을 하는 객체(프로토타입 객체)를 가리킨다.
```javascript
function Person(name) {
  this.name = name;
}

var foo = new Person('Lee');

console.dir(Person); // prototype 프로퍼티가 있다.
console.dir(foo);    // prototype 프로퍼티가 없다.
console.log(Person.__proto__ === Function.prototype); // true
console.log(Person.prototype === foo.__proto__);  //true
```
- 아직 의문점 : 프로토타입 기반의 코드를 클래스 기반으로 바꾸는 것은 쉽지만, 반대의 경우는 거의 불가능에 가깝다...?
- 참고자료
  - https://poiemaweb.com/js-prototype
  - https://poiemaweb.com/es6-class
  - https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67
  - https://medium.com/@flqjsl/js-class-%EC%99%80-prototype-%EC%9D%98-%EC%B0%A8%EC%9D%B4-7dc1d7531ae0

### this는 무엇이고, class의 super는 무엇인가??
- this
  - 단순 호출 : window 전역 객체를 가리킨다.
  - 화살표 함수 : 상위 스코프의 객체를 가리킨다. 전역 코드에서는 전역 객체를 가리킨다.
  - 객체 메서드 : 해당 객체를 가리킨다.
- super : 부모 클래스의 생성자, 메서드를 호출할 수 있는 키워드.
  - super([arguments]); // 부모 생성자 호출
  - super.functionOnParent([arguments]);
  
- 참고자료
  - https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/super
  - https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this

### SOLID - SRP 단일 책임 원칙
- 하나의 함수, 클래스는 하나의 기능만 수행해야 한다.
- 이해하기 쉽고, 유지보수가 쉬워진다.
- 계산기 클래스가 마우스 클래스의 역할을 한다고 생각해보면...
- 참고자료
  - https://cheese10yun.github.io/spring-solid-srp/

### SOLID - LSP 리스코프 교환원칙
- **"서브 타입은 언제든 자신의 기반 타입으로 교체할 수 있어야 한다. - 로버트 C 마틴"**

![lsp](https://t1.daumcdn.net/cfile/tistory/99367B345BBEF0A332)

- 위 그림과 같이 상속 관계가 논리적으로 타당하다면 LSP를 만족한다고 볼 수 있다.
- 하위 객체가 상위 객체의 역할을 하는 것에 문제가 없어야 한다는 의미.
- 참고자료
  - https://ktko.tistory.com/entry/%EC%9E%90%EB%B0%94-%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5%EC%9D%98-%EC%9B%90%EB%A6%AC-SOLID-LSP-%EB%A6%AC%EC%8A%A4%EC%BD%94%ED%94%84-%EC%B9%98%ED%99%98-%EC%9B%90%EC%B9%99
