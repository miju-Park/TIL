# ES6에서의 순회와 이터러블

## ES6의 리스트 순회

* for i++
* for of

ES5의 명령문에서 ES6의 리스트 순회는 선언적으로 표현<br/>
순회에 대해 추상화

```javascript
  const list = [1, 2, 3];
  //기존 ES5
  for (var i = 0; i < list.length; i++) {
    console.log(list([i]));
  }
  //유사배열
  const str = 'abc';
  for(var i=0; i<str.length; i++) {
    console.log(str[i])
  }

  //ES6
  for(const a of list) {
    console.log(a)
  }
  for(const a of str) {
    console.log(a)
  }
```

ES6에서 추가된 Symbol객체는 객체의 Key로 사용될 수 있다.

### Array를 통해 순회 알아보기

```javascript
  const arr = [1, 2, 3];
  for (const a of arr) {
    console.log(a);
  }
  //내부동작
  const iterator = arr[Symbol.iterator]();
  iterator.next(); //output: {value:1, done:false}
  iterator.next();
  iterator.next();
```

### Set을 통해 순회 알아보기
```javascript
  const set = new Set([1, 2, 3]);
  const iterator = set[Symbol.iterator]();
  for (const a of set) {
    console.log(a);
  }
```

### Map을 통해 순회 알아보기
```javascript
  const map = new Map([
    ["a", 1],
    ["b", 2],
    ["c", 3]
  ]);
  for (const a of map) {
    console.log(a);
  }
```

## 이터러블/이터레이터 프로토콜
* 이터러블 : 이터레이터를 리턴하는 `[Symbol.interator]()`를 가진 값<br/>
  * Array는 Symbol.iterator 함수를 가지고 있는 이터러블이다.
* 이터레이터 : {value, done} 객체를 리턴하는 `next()`를 가진 값
* 이터러블/이터레이터 프로토콜 : 이터러블을 for...of, 전개 연산자 등과 함께 동작하도록 만들어진 규약

### 사용자 정의 이터러블

```javascript
  const iterable = {
    [Symbol.iterator]() {
      let i=3;
      return {
        next() {
          return i===0 ? {done:true} : { value: i--, done: false }
        }
        [Symbol.iterator]() { return this; }
      }
    }
  };
  let iterator = iterable[Symbol.iterator]();
  iterator.next();  //{value:3, done:false}
  iterator.next();  //{value:2, done:false}
  iterator.next();  //{value:1, done:false}
  iterator.next();  //{done:true}
```

위에서 이터러블을 이터러블 프로토콜에 맞게 정의하면 <code>for...of</code>문을 사용할 수 있다.<br/>

이터러블이 반환하는 Iterator는 자기 자신을 반환하는 Well-formed Iterable이다<br/>
```javascript
  const arr = [1,2,3]
  let iterator = arr[Symbol.iterator]();
  //iterator === iterator[Symbol.iterator]()
```

### 전개 연산자

전개 연산자도 Iterator/Iterable 프로토콜을 따른다.<br/>
```javascript
  const a = [1,2];
  console.log([...a, ...[3, 4]]); //[1,2,3,4]
```
