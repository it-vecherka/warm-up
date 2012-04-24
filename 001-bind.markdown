Всем извесно, что каждая функция джаваскрипта создает отдельное пространство имен:

``` javascript
var a = 1;

function b() {
  var a = 2;
  return a;
}

b(); // returns 2
```

Также, ни для кого не секрет, что `this` у подобных функций ссылается на корневой элемент.

``` javascript
function b() {
  return this;
}

b(); // => window
```

И, в случае с функциями в качестве аргумента, переопределение `this` чревато потерей объекта:

``` javascript
User = function() {};

User.prototype.a = function(callback) {
  callback();
};

User.prototype.b = function() {
  console.log(this);
};

User.prototype.c = function() {
  this.a(this.b);
}

var u = new User();

u.c(); // => window

```

Задача: не терять `this` при передаче метода в качестве аргумента.