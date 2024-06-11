refer URL：https://pks2974.medium.com/javascript%EC%99%80-%EB%B0%98%EB%B3%B5%EB%AC%B8-67e412e9b9b9

### LOOP at javascript


#### 1
``` javascript

for(var i = 0; i < 2; i++) { console.log(i); }
// 0 1 2
var i = 0;
while(i++ < 2) { console.log(i);}
// 1 2
var i = 0;
do { console.log(i); } while(i++ < 2)
// 0 1 2

//better way for performance
var length = arr.length;
var i = 1;
for(i ; i < length; i++)

```

#### 2 for in
for( property in object ) 은 객체의 심볼이 아닌 열거 [[Enumerable]] 가능한 모든 property 을 반복 할 수 있다.

Enumerable 은 Object.defineProperty 으로 설정이 가능하다.
Array는 Array Iterator 를 반복한다.

``` javascript

for (var v in 'abc') {
  console.log(v)
}
// 0 1 2
for (var v in ['a','b','c']) {
  console.log(v)
}
// 0 1 2
for (var v in { 'a': 1,'b':2,'c':3 }) {
  console.log(v)
}
// a b c
function fn(){
    this.a = 1
    this.b = 2
    this.c = 3
}
for (var v in new fn()) {
  console.log(v)
}
// a b c

```

### 3 for of
iterables 에는 String, Array, TypedArray, Map, Set

``` javascript

for(var v of ['a','b','c']) {
  console.log(v);
}
// a b c
for(var v of 'abc') {
  console.log(v);
}
// a b c
var maps = new Map();
maps.set('a', 1).set('b', 2);
for (var v of maps) {
  console.log(v);
}
// ["a", 1] ["b", 2]
var sets = new Set()
sets.add('a').add('b')
for (var v of sets) {
  console.log(v);
}
// a b

```

### 4 for of
배열 객체를 반복하는 메서드 
Array.prototype.forEach

arr의 forEach 동작 중 arr의 참조 객체가 변경되면,
forEach의 값은 이전 참조 객체 값으로 유지 되지만,
arr의 객체의 값이 변경된다면 forEach의 값은 변경된 값이 전달된다.

``` javascript

var arr = [1,2,3,4,5]
arr.forEach((v, idx)=>{
    if (idx > 2) {
        arr = []
    } else {
        arr[idx + 1] += '' + idx
    }
    console.log(v, arr);
});
// 1  , [1, "20", 3, 4, 5]
// 20 , [1, "20", "31", 4, 5]
// 31 , [1, "20", "31", "42", 5]
// 42 , []
// 5  , []

```
