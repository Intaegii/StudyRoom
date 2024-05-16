1.Basic 

```　
function square(number) {

  console.log(arguments);
  console.log(this);

  return number * number;
}


square(2);

```　

2. 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정 X
   함수를 호출할 때 함수가 어떻게 호출되었는지에 따라 this에 바인딩할 객체가 동적으로 결정 O

```　
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

```　
foo.call(bar);   // bar
foo.apply(bar);  // bar
foo.bind(bar)(); // bar

