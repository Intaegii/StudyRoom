
## THIS


#### 1.Basic 

```javascript
function square(number) {

  console.log(arguments);
  console.log(this);

  return number * number;
}

square(2);
```javascript


2. 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정 X
   함수를 호출할 때 함수가 어떻게 호출되었는지에 따라 this에 바인딩할 객체가 동적으로 결정 O
   ※함수의 상위 스코프를 결정하는 방식인 렉시컬 스코프(Lexical scope)는 함수를 선언할 때 결정


```javascript
var foo = function () {
  console.dir(this);
};

// 1. 함수 호출
foo(); // window
// window.foo();


// 2. 메소드 호출
var obj = { foo: foo };
obj.foo(); // obj


// 3. 생성자 함수 호출
var instance = new foo(); // instance


// 4. apply/call/bind 호출
var bar = { name: 'bar' };

foo.call(bar);   // bar
foo.apply(bar);  // bar
foo.bind(bar)(); // bar
```


1. 함수 호출
  1-1. 전역객체(Global Object) - 모든 객체의 유일한 최상위 객체를 의미
   ※ 환경에 따른 최상위 객체
   　Browser-side： window,
   　Server-side(Node.js)： global
```javascript
// in browser console
this === window // true

// in Terminal
node
this === global // true
```


  1-2. 글로벌 영역에 함수를 선언한다면 전역객체의 프로퍼티(전역 변수의 메소드)로 접근가능.
```javascript
var ga = 'Global variable';

console.log(ga);
console.log(window.ga);

function foo() {
  console.log('invoked!');
}
window.foo();
```
  
