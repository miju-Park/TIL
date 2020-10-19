# 함수형 자바스크립트 기본기

## 평가

코드가 계산(Evaluation) 되어 값을 만드는 것

## 일급

* 값으로 다룰 수 잇다.
* 변수에 담을 수 있다.
* 함수의 인자로 사용될 수 있다.
* 함수의 결과로 사용될 수 있다.
```javascript
  const a = 10; //변수에 담을 수 있다.
  const add10 = a => a+10;  //함수의 인자
  const r= add10(a); //함수의 결과
  console.log(r)
```

### 일급 함수
* 함수가 값으로 다뤄질 수 있다.
* 조합성과 추상화의 도구

```javascript
  const add5 = a=>a+5;  //함수를 변수에 담을 수 있다.
  console.log(add5);  //함수의 인자로 함수를 사용할 수 있다.
  const f1 = () => () => 1; //함수의 결과값으로 함수를 사용
  console.log(f1());
```

## 고차 함수
함수를 값으로 다루는 함수

* 함수를 인자로 받아서 실행하는 함수
* 함수를 만들어 리턴하는 함수

### 함수를 인자로 받아서 실행하는 함수

```javascript
  const apply1 = (f) => f(1); // (a => a + 2 )(1)
  const add2 = (a) => a + 2;
  console.log(apply1(add2)); //3
```
```javascript
  const times = (f, n) => {
    let i = -1;
    while (++i < n) f(i);
  };
  times(console.log, 3);
```

### 함수를 리턴하는 함수

함수를 리턴하는 함수는 클로저를 리턴하는 함수.<br/>
아래 addMaker에서 리턴하는 함수 <code>b => a + b </code>는 함수 인자 <code>a</code>를 기억하는 클로저이다.
```javascript
const addMaker = (a) => (b) => a + b;
const add10 = addMaker(10);
console.log(add10(5));
```