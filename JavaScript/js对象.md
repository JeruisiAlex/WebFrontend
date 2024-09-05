# js 对象

## 基本认识

- 在 JavaScript 中，除了原始值，万物皆是对象。
  - 下面这些数据类型都是对象
    - 布尔是对象（如果用 *new* 关键词定义）
    - 数字是对象（如果用 *new* 关键词定义）
    - 字符串是对象（如果用 *new* 关键词定义）
    - 日期永远都是对象
    - 算术永远都是对象
    - 正则表达式永远都是对象
    - 数组永远都是对象
    - 函数永远都是对象
    - 对象永远都是对象
  - **原始值**指的是没有属性或方法的值。
  - **原始数据类型**指的是拥有原始值的数据。JavaScript 定义了 5 种原始数据类型：
    - string
    - number
    - boolean
    - null
    - undefined
- JavaScript 对象是**命名值**的集合包含了属性和方法。
  - **属性**是 js 对象中的命名值。
    - 对象属性可以是原始值、其他对象以及函数。
  - **方法**是可以在对象上执行的动作。
    - **对象方法**是包含*函数定义*的对象属性。
- JavaScript 中对于对象的拷贝都是浅拷贝，即复制的对象的地址，因此改变拷贝后的对象，拷贝前的对象也会改变。

## 创建对象

在 JavaScript 中有三种方法来创建对象

- 定义和创建单个对象，使用对象文字。
- 定义和创建单个对象，通过关键词 new。
- 定义对象构造器，然后创建构造类型的对象。

```js
// 使用对象文字，即 {} 中的键值对来创建对象
let person = {firstName:"Bill", lastName:"Gates", age:62, eyeColor:"blue"}; 

// 使用 new 关键词
let person = new Object();
person.firstName = "Bill";
person.lastName = "Gates";
person.age = 50;
person.eyeColor = "blue"; 

// 对象构造器将在后面介绍
```

## 对象的属性

### 访问方式

访问对象属性的语法是：

```js
objectName.property           // person.age
```

或者：

```js
objectName["property"]       // person["age"]
```

或者：

```js
objectName[expression]       // x = "age"; person[x]
```

表达式必须计算为属性名。

### 添加属性

通过赋值，可以直接向已存在的对象添加新的属性。

```js
person.nationality = "English";
```

### 删除属性

使用 `delete` 关键字从对象中删除属性。

```js
var person = {firstName:"Bill", lastName:"Gates", age:62, eyeColor:"blue"};
delete person.age;   // 或 delete person["age"];
```

### 原型属性

JavaScript 对象继承了它们的原型的属性。`delete` 关键词不会删除被继承的属性，但是如果您删除了某个原型属性，则将影响到所有从原型继承的对象。

## 对象的方法

JavaScript 中对象的**方法**是包含**函数定义**的属性。

### 创建对象的方法

```js
methodName : function() { 代码行 }
```

### 访问对象的方法

```js
objectName.methodName()
```

- 通常把 fullName() 描述为 person 对象的方法，把 fullName 描述为属性。
- fullName 属性在被通过 () 调用后会以函数形式执行。
- 如果访问 fullName **属性**时没有使用 ()，则将返回**函数定义**。

## 对象的转化

- 使用 Object.values() 的方法可以将对象中的属性转化为数组。
- 使用 JSON.stringify() 可以将对象转化为字符串，结果将是一个遵循 JSON 标记法的字符串，并且这种字符串可以转回对象。需要注意的是，方法并不会被转化为字符串的一部分，除非提前使用 toString() 将方法转化为字符串。

## 对象访问器

### 对访问器的基本认知

- JavaScript 中也存在类似 Java 的 Getter 和 Setter，这两者即是对象访问器。
  - 但是这种访问器与 Java 是存在区别的。
    - Java 中的 Getter 和 Setter 主要的作用之一是用于对私有属性的封装，但是 JavaScript 中不存在私有属性和公开属性的概念。
    - 同时 Java 中的 Getter 和 Setter 本质还是方法，但是 JavaScript 中的 Getter 和 Setter 调用形式更像是属性的调用。
  - 即使有 Getter 和 Setter 依然可以直接改变属性的值，那么 JavaScript 中 Getter 和 Setter的意义是什么呢？
    - 一方面这样可以增强代码的复用性，将一些赋值时需要进行的重复操作封装起来。
    - 另一方面可以像调用属性一样调用，会比调用函数看起来更加简洁。
  - 那么有什么缺陷吗？
    - 一方面 Setter 只能有一个参数，有一定的局限性。
    - 另一方面 

### 添加访问器的方法

- 添加 Getter

```js
// 创建对象：
var person = {
  firstName: "Bill",
  lastName : "Gates",
  language : "en",
  get lang() {
    return this.language;
  }
};
```

- 添加 Setter

```js
var person = {
  firstName: "Bill",
  lastName : "Gates",
  language : "",
  set lang(lang) {
    this.language = lang;
  }
};

// 使用 setter 来设置对象属性：
person.lang = "en";
```

- 通过 `Object.defineProperty()` 方法也可用于添加 Getter 和 Setter

```js
var obj = {counter : 0};

// 定义 setters
Object.defineProperty(obj, "reset", {
  get : function () {this.counter = 0;}
});
Object.defineProperty(obj, "increment", {
  get : function () {this.counter++;}
});
Object.defineProperty(obj, "decrement", {
  get : function () {this.counter--;}
});
Object.defineProperty(obj, "add", {
  set : function (value) {this.counter += value;}
});
Object.defineProperty(obj, "subtract", {
  set : function (value) {this.counter -= value;}
});
```

## 对象构造器

### 构造器的作用

- 很多时候我们都需要创建需要相同类型的对象，这个是用就需要是用**构造器**来进行快速构建。

### 如何创建构造器

- 创建构造器就是编写一个函数，然后使用 new 关键字搭配函数名称即可创建新的对象。

```js
function Person(first, last, age, eye) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eye;
}

let myFather = new Person("Bill", "Gates", 62, "blue");
let myMother = new Person("Steve", "Jobs", 56, "green");
```

- 通过上面这个例子可以看到，你可以将任何函数视作对象构造器，并使用 new 关键字来构造对象。
  - 但是请注意，只有函数中使用 `this.` 这样的语法的才能声明属性和方法或者使用 Getter 或 Setter 才能声明方法。
- 关于 `this` :
  - 在 JavaScript 中，被称为 `this` 的事物是代码的“拥有者”
  - `this` 的值，在对象中使用时，就是对象本身。
  - 在构造器函数中，`this` 是没有值的。它是新对象的替代物。 当一个新对象被创建时，`this` 的值会成为这个新对象。
  - 请注意 `this` 并不是变量。它是关键词。

## 对象原型

- **在 JavaScript 中所有的对象都从原型继承属性和方法**。

### 什么是原型

- 前文提到，每一个函数都可以看作构造器。每一个函数也都具有一个属性叫做 `prototype`，这个属性指向一个对象，这个对象就是该构造函数的原型。
- 同时，每个对象还有一个属性 `__proto__`，这个属性也指向一个对象，这个对象就是它的构造函数的 `prototype` 属性指向的对象。该属性指向的对象就是这个对象的对象原型。

### 有什么作用

- 所有的对象都从它的原型处继承属性和方法。
- 对于一个已经确定的构造函数，我们无法通过下面的形式去添加任何的属性和方法：

```js
function Person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}
Person.nationality = "English";
```

- 但是我们可以通过原型来维他为构造函数添加属性和方法：

```js
function Person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}
Person.prototype.nationality = "English";
```

- 关于原型，会在 `JavaScript原型链` 中进行详细的介绍。