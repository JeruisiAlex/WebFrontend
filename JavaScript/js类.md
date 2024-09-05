# js 类

- 类是对象的模板，这一点在 Java 中得到了很好的体现，而在 JavaScript 中，也是差不多的。

## 类的创建

- 通过关键字 class 创建一个类，也记得始终为类添加一个 constructor() 方法，这是该类的构造方法，用于构造对象。

```js
class Car {
  constructor(name, year) {
    this.name = name;
    this.year = year;
  }
}

let myCar1 = new Car("Ford", 2014);
let myCar2 = new Car("Audi", 2019);
```

- 构造方法的名称必须是 `constructor`，如果没有添加构造方法，则系统会自动添加一个空的构造方法。
- 构造方法中通过 `this` 声明的变量即为对象的属性。
- 类中可以声明任意个带任意数量参数的方法。
- 类的声明不会被提升。
- 类中也可以声明 Getter 和 Setter，方式与构造器函数中类似。

## 类的继承

- 通过 `extends` 关键字，可以让一个类继承另一个类的属性和方法。被继承的类称为父类，继承的类称为子类。
- 子类拥有父类的所有属性和方法，如果在子类中命名同样的方法会覆盖父类原本的方法。
- 通过 `super` 可以在子类中调用父类的方法。

```js
class Car {
  constructor(brand) {
    this.carname = brand;
  }
  present() {
    return 'I have a ' + this.carname;
  }
}

class Model extends Car {
  constructor(brand, mod) {
    super(brand); // 调用父类 Car 的构造方法
    this.model = mod;
  }
  show() {
    return this.present() + ', it is a ' + this.model;
  }
}

let myCar = new Model("Ford", "Mustang");
document.getElementById("demo").innerHTML = myCar.show();
```

## 静态方法

- 通过 `static` 关键字可以声明静态方法，这样的方法不能被该类的对象调用，但是可以直接通过 `类名.方法名` 的方式调用。
- 静态方法中不能使用对象的属性。

```js
class Car {
  constructor(name) {
    this.name = name;
  }
  static hello() {
    return "Hello!!";
  }
}

let myCar = new Car("Ford");

// 您可以在 Car 类上调用 'hello()' ：
document.getElementById("demo").innerHTML = Car.hello();

// 但不能在 Car 对象上调用：
// document.getElementById("demo").innerHTML = myCar.hello();
// 此举将引发错误。
```
