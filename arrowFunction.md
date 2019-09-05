```javascript
function foo(){
    this.val = 3
}

foo.prototype = {
    setValFunc: function (x) {
        this.val = x
    },
    setValArrow: (x) => {
        this.val = x
    },
    getValFunc: function () {
        return this.val
    },
    getValArrow: () => {
        return this.val
    }
}

const obj = new foo()
console.log(obj.getValArrow()) // undefined
console.log(obj.getValFunc()) // 3

obj.setValArrow(450)
console.log(obj.getValArrow()) // 450
console.log(obj.getValFunc()) // 3

obj.setValFunc(111)
console.log(obj.getValArrow()) // 450
console.log(obj.getValFunc()) // 111
```

### 의문점 - 화살표 함수의 this는 무엇을 가리키는 것인가??

마지막줄에 코드를 추가해 테스트를 해봤다.

```javascript
const obj2 = new foo()
console.log(obj2.getValArrow()) // 450
console.log(obj2.getValFunc()) // 3
```

### 결론
- 화살표 함수의 this가 뭔지는 정확히 모르겠으나, this에 접근해야 할 때 사용할 일은 없을 듯 하다.
- prototype 메서드는 일반 함수로 사용하는 것이 좋겠다