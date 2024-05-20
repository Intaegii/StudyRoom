reference URL :
https://blog.naver.com/minis24/80094326463
https://velog.io/@ken1204/%EA%B0%9D%EC%B2%B4-%EB%A6%AC%ED%84%B0%EB%9F%B4-10

### Javascript에서의 객체
・JS는 객체 기반의 프로그래밍 언어이며, JS를 구성하는 거의 '모든 것'이 객체다.
・원시 값을 제외한 나머지 값(함수, 배열, 정규 표현식 등)은 모두 객체다</br>
```
원시 값은 변경 불가능(immutable) / 객체는 변경 가능한 값(mutable)
```
</br>

・JS에서 사용할 수 있는 모든 값은 프로퍼티 값이 될 수 있다.
・함수도 프로퍼티 값으로 사용할 수 있는데, 이런 경우 일반 함수와 구분하기 위해 메소드(method)라 부른다.
```
이처럼 객체는 프로퍼티와 메서드로 구성된 집합체다. 프로퍼티와 메서드의 역할은 다음과 같다.
```
・프로퍼티: 객체의 상태를 나타내는 값(data)
・메소드: 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작(behavior)
이처럼 객체는 상태와 동작을 하나의 단위로 구조화할 수 있어 유용하다.
</br>

### 객체 리터럴에 의한 객체 생성
```
C++나 자바 같은 클래스 기반 객체지향 언어는 클래스를 사전에 정의하고 필요한 시점에 new 연산자와 함께 생성자(constructor)를 호출하여 인스턴스를 생성하는 방식으로 객체를 생성한다.
그렇다면 JS는?
```

・JS는 프로토타입 객체지향 언어 - 클래스 뿐만 아니라 다양한 객체 생성 방법 지원
・그 중 가장 대표적인 객체 리터럴 방식const object={}은 객체를 생성하기 위해 클래스를 먼저 정의하고 new 연산자와 함께 생성자를 호출할 필요가 없다. (숫자값, 문자값 생성 방식과 유사)
・객체 리터럴 외의 객체 생성 방식은 모두 함수를 사용해 객체 생성

### * 초기화 하는 방법 두가지 </br>

#### 1. 객체의 리터럴 (값) 
```
        var empty = {};                                     // 빈객체
        var point = {x : 0 , y : 0};                        //point.x = 0 , point.y = 0
        var human = { "name" : "Homer",
                             "age" : 34 ,
                             "married" : true};

        // 프로퍼티는 식별자나 "문자열" 이 올수 있다.        
        // 객체의 리터럴은 자바스크립트 표현식으로서, 평가될때 마다 새로운 객체를 생성하고 초기화 시킨다.</br>
```
 

#### 2. new 연산자 이용  </br>
```
       var a = new Array()           // 빈배열 생성
       var o = new Object()          // 빈객체 생성  
       // var o = {}     
```
 </br>
 
### 프로퍼티(속성)
```
객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.
```
 </br>
 
####　식별자 네이밍 규칙

```
・프로퍼티 키: 빈 문자열을 포함하는 모든 문자열 또는 심벌 값
・프로퍼티 값: JS에서 사용할 수 있는 모든 값
```
 </br>
 
・식별자 네이밍 규칙을 따르지 않는 프로퍼티 키를 사용하면 번거로운 일이 발생한다. 가급적 따를 것을 권장함.

```
var person = {
  firstName: 'Ung-mo', // 식별자 네이밍 규칙을 준수하는 프로퍼티 키
  'last-name': 'Lee'   // 식별자 네이밍 규칙을 준수하지 않는 프로퍼티 키
};


console.log(person); // {firstName: "Ung-mo", last-name: "Lee"}
var person = {
  firstName: 'Ung-mo',
  last-name: 'Lee' // SyntaxError: Unexpected token -
};
```
 </br>

・JS엔진은 last-name을 -연산자가 있는 표현식으로 해석한다.
```
var obj = {};
var key = 'hello';

// ES5: 프로퍼티 키 동적 생성
obj[key] = 'world';
// ES6: 계산된 프로퍼티 이름
// var obj = { [key]: 'world' };

console.log(obj); // {hello: "world"}
```
 </br>
 
・문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다.
・이 경우에는 프로퍼티 키로 사용할 표현식을 대괄호[]로 묶어야 한다.

```
var foo = {
  '': ''  // 빈 문자열도 프로퍼티 키로 사용할 수 있다.
};

console.log(foo); // {"": ""}
```
 </br>
 
・빈 문자열도 프로퍼티 키로 사용할 수 있지만 권장하지 않는다.
```
var foo = {
  0: 1,
  1: 2,
  2: 3
};

console.log(foo); // {0: 1, 1: 2, 2: 3}
```
 </br>
 
・프로퍼티 키에 문자열이나 심벌 값 외의 값을 사용하면 암묵적 타입 변환을 통해 문자열이 된다.
```
var foo = {
  name: 'Lee',
  name: 'Kim'
};

console.log(foo); // {name: "Kim"}
```

・이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다. 이 때 에러가 발생하지 않는다는 점에 주의하자.

### 메서드
・JS에서 사용할 수 있는 모든 값은 프로퍼티 값으로 사용 가능
・JS 함수는 객체다. - 따라서 함수는 값으로 취급할 수 있기 때문에 프로퍼티 값으로 사용할 수 있다. - 이 경우를 메서드라고 부른다.
```
var circle = {
  radius: 5, // ← 프로퍼티

  // 원의 지름
  getDiameter: function () { // ← 메서드
    return 2 * this.radius; // this는 circle을 가리킨다.
  }
};

console.log(circle.getDiameter()); // 10
```

・메서드 내부에서 사용한 this 키워드는 객체 자신(위 예제에서는 circle 객체)을 가리키는 참조변수다. 
 </br>
 
### 프로퍼티 접근
・프로퍼티에 접근하는 방법에는 두 가지가 있다

//마침표.와 대괄호[]

* 연관 배열로서의 객체
   - 배열에서 사용되는 [] 연산자를 사용해도 객체의 프로퍼티에 접근 할 수 있다.
     즉 , object.property  와 object["property"] 는 같다.
   - 이런 형태로 객체를 사용할 때 연관배열이라고 한다.
   ※ [] 연산자안의 프로퍼티가 문자열 형태이기 때문에 런타임시에 동적으로 컨트롤 할 수 있다.


객체의 공통 메서드 및 프로퍼티

   - 모든 객체는 Object 클래스를 상속하며, 각자의 고유한 프로퍼티와 메서드가 있으며,
      Object 클래스에서 상속 받은 공통의 메서드와 프로퍼티가 있다.

      1. constructor 프로퍼티
　　　　# 모든 객체는 생성자 함수를 가치키는 constructor 프로퍼티를 가지고 있다.
              ex ) Date() 생성자로 생성된 d 객체는 d.constructor 프로퍼티가 있다.
                  d.constructor 은 Date 를 가리킨다.
```
                  var d = new Date() ;
                  d.constructor == Date ;                     // true
```

　　※ instanceof  연산자는 constructor 프로퍼티 값을 사용한다.

```
                 d.constructor == Date ;                     //true
                 d instanceof Date ;                           //true


```

     2. valueOf() 메서드
       　# 자바스크립트가 객체를 문자열이 아니라 숫자 같은 다른 기본타입으로 변환하려 할때 호출된다.
         # Object 클래스가 기본제공하는 valueOf() 는 이런 변환을 수행하지 않는다.
              각 객체의 클래스에서 오버라이드 하여 사용한다.
         # 몇몇 내장 객체는 자신만의 valueOf()메서드를 정의하고 있다.
               ex) Date.valueOf();

     3. toString() 메서드  
         # 메서드를 호출한 객체의 값을 어떠한 방식으로든 표현하는 문자열을 만들어 리턴한다.
         # 기본 제공하는 toString() 메서드는 "[Object object]"

    4.hasOwnProperty() 메서드
        # 프로퍼티의 이름을 담는 한개의 문자열 인자를 받는다 객체가 이 프로퍼티를 소유하고 있는지 검사
        ※ 프로퍼티가 지역적으로 정의되어있으면 true 리턴
        ※ 상속받은 프로퍼티 이거나, 존재하지 않으면 false 리턴
        
        
```
             var o = {} ;
             o.hasOwnProperty("undef");                   // false(존재하지 않는 프로퍼티)
             o.hasOwnProperty("toString");                // false(상속 받은 프로퍼티)
             Math.hasOwnProperty("cos");                // true
```

       5. isPrototypeOf() 메서드
         # 이 메서드의 객체가 전달인자로 주어진 객체의 프로토 타입 객체이면 true 리턴
           그렇지 않으면 false 리턴

```   
         var o = {} ;
           Object.prototype.isPrototypeOf(o)             // true
             // o.constructor == Object ;  이값이 true 이고,
             // o의 클래스는 Object 이다  new Object() == {}

         Function.prototype.isPrototypeOf(Object)         //true
          // Object.prototype == Function  (외우세요)

 

var person = {
  name: 'Lee'
};

// 마침표 표기법에 의한 프로퍼티 접근
console.log(person.name); // Lee

// 대괄호 표기법에 의한 프로퍼티 접근
console.log(person['name']); // Lee
```


・대괄호 표기법을 사용하는 경우 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 한다.
```
var person = {
  name: 'Lee'
};

console.log(person[name]); // ReferenceError: name is not defined

// 이런 참조 에러를 발생시킬 수 있다.
```
 </br>
・위 예제에서 참조 에러가 발생한 이유는 대괄호 연산자 내의 따옴표를 감싸지 않은 이름, 즉 식별자 name을 평가하기 위해 선언된 name을 찾았지만 찾지 못했기 때문이다.

```
var person = {
  name: 'Lee'
};

console.log(person.age); // undefined
```

 </br>
・객체에 존재하지 않는 프로퍼티에 접근하면 undefined를 반환한다. 이 때 참조에러가 발생하지 않는다!

```
var person = {
  'last-name': 'Lee',
  1: 10
};

person.'last-name';  // -> SyntaxError: Unexpected string
person.last-name;    // -> 브라우저 환경: NaN
                     // -> Node.js 환경: ReferenceError: name is not defined
person[last-name];   // -> ReferenceError: last is not defined
person['last-name']; // -> Lee

// 프로퍼티 키가 숫자로 이뤄진 문자열인 경우 따옴표를 생략할 수 있다.
person.1;     // -> SyntaxError: Unexpected number
person.'1';   // -> SyntaxError: Unexpected string
person[1];    // -> 10 : person[1] -> person['1']
person['1'];  // -> 10

```
 </br>

위 예제에서 person.last-name의 실행결과가 브라우저 환경과 Node.js 환경에서 서로 다르다. 왜?

・person.last-name을 실행할 때 JS 엔진은 먼저 person.last를 평가한다.

・person객체에는 프로퍼티 키가 last인 프로퍼티 키가 없기 때문에 person.last는 undefined로 평가된다.

・따라서 person.last-name은 undefined-name과 같다.

・다음으로 JS 엔진은 name이라는 식별자를 찾는다. 이 때 name은 프로퍼티 키가 아니라 식별자로 해석된다.

・Node.js 환경에서는 현재 어디에도 name이라는 식별자(변수, 함수 등의 이름) 선언이 없으므로 ReferenceError: name is not defined라는 에러가 발생한다.

・그런데 브라우저 환경에서는 name이라는 전역 변수(전역 객체 window의 프로퍼티)가 암묵적으로 존재한다.

・따라서 전역 변수 name은 window의 이름을 가리키며, 기본값은 빈 문자열이다.

・결과적으로, person.last-name은 undefined - ''와 같으므로 NaN이 된다.


#### 프로퍼티 동적 생성
```
var person = {
  name: 'Lee'
};

// person 객체에는 age 프로퍼티가 존재하지 않는다.
// 따라서 person 객체에 age 프로퍼티가 동적으로 생성되고 값이 할당된다.
person.age = 20;

console.log(person); // {name: "Lee", age: 20}
```
・존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.


#### 프로퍼티 삭제
* 프로퍼티의 삭제
   - delete 연산자 사용
     실제로 객체에서 프로퍼티를 완전히 제거한다.

```
var person = {
  name: 'Lee'
};

// 프로퍼티 동적 생성
person.age = 20;

// person 객체에 age 프로퍼티가 존재한다.
// 따라서 delete 연산자로 age 프로퍼티를 삭제할 수 있다.
delete person.age;

// person 객체에 address 프로퍼티가 존재하지 않는다.
// 따라서 delete 연산자로 address 프로퍼티를 삭제할 수 없다. 이때 에러가 발생하지 않는다.
delete person.address;

console.log(person); // {name: "Lee"}
```
・delete 연산자는 객체의 프로퍼티를 삭제한다.
・만약 존재하지 않는 프로퍼티를 삭제하면 아무런 에러 없이 무시된다.

#### 계산된 프로퍼티 이름
```
// ES5
var prefix = 'prop';
var i = 0;

var obj = {};

// 계산된 프로퍼티 이름으로 프로퍼티 키 동적 생성
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
// ES6
const prefix = 'prop';
let i = 0;

// 객체 리터럴 내부에서 계산된 프로퍼티 이름으로 프로퍼티 키 동적 생성
const obj = {
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i
};

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
```

・ES6에서는 객체 리터럴 내부에서도 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성할 수 있다.

#### 메서드 축약
```
ES5에서 메서드를 정의하려면 프로퍼티 값으로 함수를 할당한다.
// ES5
var obj = {
  name: 'Lee',
  sayHi: function() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee
ES6에서는 메서드를 정의할 때 축약 가능
// ES6
const obj = {
  name: 'Lee',
  // 메서드 축약 표현
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee
```
