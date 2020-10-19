# 제너레이터와 이터레이터

## 제너레이터/이터레이터

* 제너레이터 : 이터레이터이자 이터러블을 생성하는 함수. 즉 이터레이터를 리턴하는 함수<br/>

```javascript
  function *gen(){
    yield 1;
    yield 2;
    yield 3;
    return 100; //next() 호출시 마지막에 {value:100, done:true}
  }
  let iterator = gen();
  iterator.next();
  iterator.next();
  iterator.next();

  for( const a of gen()) console.log(a) 
    //순회할 때는 마지막 return값은 제외하고 순회가 이뤄짐
```

제너레이터를 통해 쉽게 이터레이터를 만들 수 있다<br/>
<code>yield</code>를 통해 얼마나/무엇을 순회할 지 결정할 수 있고, 문장으로 순회할 값을 표현한다.<br/>
Generator를 통해서 어떠한 값이나 상태를 순회할 수 있는 형태로 만들 수 있다.

## 제너레이터 활용(odds)

홀수만 발생시키는 Iterator를 순회<br/>
```javascript
  function *infinity(i = 0) {
    //무한히 값을 생성하지만, 평가할때까지만 동작하기 때문에 멈추는 일은 없음
    while(true) yield i++;
  }
  function *limit(_limit, iter) {
    for(const a of iter) {
      yield a;
      if( a === _limit ) return;
    }
  }
  function *odds(_limit) {
    for(const a of limit(limit, infinity(1))) {
      if( a % 2 ) yield a;
      if( a === _limit ) return;
    }
  }
  let iter2 = odds(10);
  console.log(iter2.next())
  console.log(iter2.next())
  console.log(iter2.next())
  console.log(iter2.next())

```

### for...of, 전개 연산자, 구조 분해, 나머지 연산자
Generator 연산자는 Iterator 프로토콜을 따르고 있기 때문에 <code>for...of</code>, 전개 연산자, 구조 분해, 나머지 연산자 등을 사용할 수 있다.<br/>
```javascript
  console.log(...odds(10)); //1 3 5 7 9
  console.log([...odds(10), ...odds(20)])

  const [head, ...tail] = odds(5);
  console.log(head);  //1
  console.log(tail);   //[3,5]

  [const a, b, ...rest] = odds(10);
  console.log(a); //1
  console.log(b); //3
  console.log(rest);  //[5,7,9]

```