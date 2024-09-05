# js 函数

函数，一段封装起来的用于执行重复性任务的代码。

## 函数定义

- 最基本的定义方式，这样声明的函数会被提升。

```js
function functionName(parameters) {
   要执行的代码
}
```

- 函数表达式，即将函数赋值给一个变量，这样声明的函数与变量一样，不会被提升。

```js
var x = function (a, b) {return a * b}
var z = x(4, 3)
```

- Function() 构造器，实际上这种方法并不好用，完全不需要使用

```js
var myFunction = new Function("a", "b", "return a * b")
var x = myFunction(4, 3)
```

- 自调用函数，即这个函数在被定义时就调用一次，之后无法再被调用

```js
(function () {
    var x = "Hello!!";      // 我会调用我自己
})();
```

- 箭头函数，允许使用简短的语法来编写函数表达式。但是箭头函数没有自己的 this，不适合定义对象方法。

```js
const x = (x, y) => { return x * y }
```

- 注意，就像 `js 对象` 中写到的一样，在 JavaScript 中，万物都是对象，函数也是，因此函数是有自己的属性和方法的。

## 函数参数

- 函数拥有参数
  - **函数形参（parameter）**指的是在函数定义中列出的*名称*。
  - **函数实参（argument）**指的是传递到函数或由函数接收到的真实*值*。

```js
functionName(parameter1, parameter2, parameter3) {
    要执行的代码
}
```

- 在 JavaScript 中调用函数时传递参数是比较自由的，传递参数的数量可以少于函数的形参数量，也可以多于形参数量，这一点相比 C 或者 Java 来说无疑是更自由的，但是它并不像 Python 那样可以指定传递给哪些形参，他只会按照顺序赋值。

  - 如果实参数量少于形参，那么未被赋值的形参值会是 undefined，可以通过下面这样的形式来给形参赋予默认值（这一点上是不是很方便的）

  ```js
  function myFunction(x, y) {
      if (y === undefined) {
            y = 0;
      } 
  }
  ```

  - 如果实参数量多于形参，那么多于的参数可以通过函数的内置对象 **arguments** 来获得，下面是一个例子。

  ```js
  x = findMax(1, 123, 500, 115, 44, 88);
  
  function findMax() {
      var i;
      var max = -Infinity;
      for (i = 0; i < arguments.length; i++) {
          if (arguments[i] > max) {
              max = arguments[i];
          }
      }
      return max;
  }
  ```

## 函数调用

- 在调用函数的时候有一个最重要的问题，就是 `this` 这个关键字到底指代的是什么，普遍来说，`this` 指代调用这个函数的对象。

- 对于写在最外层的函数，其实他们都属于 HTML 页面这个对象，即浏览器窗口 window，因此这样的函数的 this，就是指向的 window 这个对象。

```js
function myFunction(a, b) {
    return a * b;
}
window.myFunction(10, 2);    // 也会返回 20
```

- 而对于对象内部的方法函数，this 则是指的这个对象。

- 需要注意的是，作为构造器的函数内的 this 关键词是没有值的。

## 改变函数调用时的 this

### call() 方法

这是 JavaScript 内置的一个方法可以用来改变当次调用时的 this 指向的对象，具体表现为 call 的第一个参数即是 this 指向的对象。具体的用法可以参考下面这个例子。

```js
var person = {
  fullName: function(city, country) {
    return this.firstName + " " + this.lastName + "," + city + "," + country;
  }
}
var person1 = {
  firstName:"Bill",
  lastName: "Gates"
}
person.fullName.call(person1, "Seattle", "USA");
```

### apply() 方法

该方法与 call() 几乎一致，唯一的区别在于调用时参数传入是通过一个数组传递的，而不是像 call() 一样是一个一个参数传递。详情可以参考下面这个例子。

```js
var person = {
  fullName: function(city, country) {
    return this.firstName + " " + this.lastName + "," + city + "," + country;
  }
}
var person1 = {
  firstName:"Bill",
  lastName: "Gates"
}
person.fullName.apply(person1, ["Oslo", "Norway"]);
```

- **注意，无论是 call() 还是 apply() 都只是改变当次调用的 this 指向的对象，再次调用时，this 还是会指向它默认的对象**。

### bind() 方法

通过使用 bind() 方法，一个对象可以从另一个对象借用一个方法。不同于 call() 以及 apply()，通过 bind() 为方法绑定新的对象之后，对之后的每次调用都是生效的。

在下面这个例子中，这是没有通过 bind 来绑定对象的代码，这样会导致最后显示出来的内容是 undefined。

```js
const person = {
  firstName:"Bill",
  lastName: "Gates",
  display: function () {
    let x = document.getElementById("demo");
    x.innerHTML = this.firstName + " " + this.lastName;
  }
}

setTimeout(person.display, 3000);
```

通过 bind 绑定之后就可以正常显示，避免回调函数中 this 的丢失是 bind 的一个重要作用。

```js
const person = {
  firstName:"Bill",
  lastName: "Gates",
  display: function () {
    let x = document.getElementById("demo");
    x.innerHTML = this.firstName + " " + this.lastName;
  }
}

let display = person.display.bind(person);
setTimeout(display, 3000);
```

## 闭包

- 如果系统的学习过 C 系列语言或者编译原理，那么作用域这个概念一定不会陌生。
- 在一段代码中，处于最外层的的变量被称为全局变量，而处于函数内部的被称为局部变量。全局变量所处于的作用域是最外层的作用域，而每进入一个函数就相当于进入了一个更小的作用域，小的作用域被更大的作用域通过 `{}` 包围起来，小的作用域中可以调用在大的作用域甚至更大的作用域中声明的变量函数，但是大的作用域不能调用内部的作用域里面声明的变量函数。
- 对于重名的变量，小的作用域中的变量会隐藏外面作用域中的同名变量。

```js
// 初始化计数器
var counter = 0;

// 递增计数器的函数
function add() {
  counter += 1;
}

// 调用三次 add()
add();
add();
add();

// 此时计数器应该是 3
```