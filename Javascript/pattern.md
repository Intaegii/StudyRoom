## Javascript Pattern </br>

#### NameSpace Pattern

```
// anti pattern : change before 
// global vairable 5개
function Parent() {
}
function Child() {
}
var some_var = 1;
var module1 = {};
var module2 = {};

// change after 
var MYAPP = {};
MYAPP.Parent = function() {

};
MYAPP.Child = function() {

};
MYAPP.some_var = 1;

MYAPP.modules = {};
MYAPP.modules.module1.data = {a:1, b:2};
MYAPP.modules.module2 = {};

```
