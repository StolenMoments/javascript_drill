# 자바스크립트 private member 고찰

자바스크립트는 기본적으로 private member를 제공하지 않는다.

그렇다면 멤버 변수를 메서드로만 변화를 줄 수 있게끔 만들고 싶은데 어떻게 하나..?
<br><br>


### 고민 과정
- Object.freeze() 라는 녀석이 있네. 이걸로 비벼볼까? -> 한 번 얼리면 변경이 절대 불가능하다. 삽질.
- Naming Convention :  실질적인 제한이 이뤄지지 않으니 패스.
- Symbol, WeakMap 활용 : 그나마 괜찮아 보이는 방법인데 손이 안간다...나중에 해보기.

<br>

한참 고민하고 구글링하며 방법을 찾았다.

### 함수 안에 변수를 넣기

```javascript
function foo() {
    let name = "HELLO"

    this.getName = function (){
        return name
    }
    
    this.setName = function (x){
         name = x
    }
}

const test = new foo()

console.log(test.getName()) // "HELLO"
test.name = "111"
console.log(test.getName()) // "HELLO"

test.setName("WORLD")
console.log(test.getName()) // "WORLD"

console.log(test) // foo { getName: [Function], name: '111' }
```

test.name = "111" 코드가 실행이 됐을 때, 멤버 변수 name이 추가되는 것을 볼 수 있다.

하지만 보호하고 싶은 foo() 안의 name 은 여전히 의도한 값을 가지고 있다.

완벽하진 않지만 만족할 만한 결과를 얻었다.

새로운 property가 생성되는 것에 대한 고민을 해봐야겠다.


### 클래스는 어떻게 할 것인가?

네이밍 컨벤션 (변수명 앞에 언더바 붙이는 식), Symbol, WeakMap 을 사용한 방법이 있었다.

**ES2019** 부터는 '#'을 이용해 private member를 정의할 수 있다.

```javascript
class Person {
    #name; // 안해주면 에러 발생 (Private field '#name' must be declared in an enclosing class)
    constructor() {
        this.#name = "NAME";
    }

    getName() {
        return this.#name;
    }
}

console.log(new Person().getName()); // "NAME"
```




# 참고 자료
https://stackoverflow.com/questions/22156326/private-properties-in-javascript-es6-classes

https://gomugom.github.io/how-to-make-private-member/

http://chanlee.github.io/2013/12/10/understand-javascript-closure/

http://javascriptissexy.com/understand-javascript-closures-with-ease/

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes/Private_class_fields
