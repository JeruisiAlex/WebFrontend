# JavaScript 基础知识

- JavaScript 简称 JS，后续这两个称呼会混着使用。

- JS 比较类似于一种脚本语言，用来控制 HTML 元素，也可以控制 HTML 元素的 CSS 样式。
- JS 必须写在 \<Script> 标签内。

## JS 输出

- `innerHTML` 用于改变元素内部的内容。

```html
<!DOCTYPE html>
<html>
<body>

<h1>我的第一张网页</h1>

<p>我的第一个段落</p>

<p id="demo"></p>

<script>
 document.getElementById("demo").innerHTML = 5 + 6;
</script>

</body>
</html> 
```

- `document.write()`用于直接向 HTML 文档中的 \<body> 写入内容。
  - 需要注意的是，如果 HTML 文档已经加载完毕了，再使用 `document.write()` 会清空 HTML 文档中的所有内容。类似于C语言打开一个文件向里面写入这种情况。

```html
<!DOCTYPE html>
<html>
<body>

<h1>我的第一张网页</h1>

<p>我的第一个段落</p>

<button onclick="document.write(5 + 6)">试一试</button>

</body>
</html>
```

- `window.alert()` 弹出一个带有信息的警示框。

```html
<!DOCTYPE html>
<html>
<body>

<h1>我的第一张网页</h1>

<p>我的第一个段落</p>

<script>
window.alert(5 + 6);
</script>

</body>
</html>
```

- `console.log()` 向控制台输出内容，一般 debug 用的最多的。

```html
<!DOCTYPE html>
<html>
<body>

<h1>我的第一张网页</h1>

<p>我的第一个段落</p>

<script>
console.log(5 + 6);
</script>

</body>
</html>
```

## JS 变量

### 变量声明

- JS 是一种类似于脚本语言的语言，与 Python 类似它的变量并不会在声明的时候指定数据类型，而是在第一次赋值之后确定数据类型。
- JS 中有三种可以用来声明变量的关键字 `var`, `let`, `const`
- `var` 可以用来声明一个变量。
  - 但是 `var` 在现在的版本里面并不推荐使用，因为通过 `var` 声明的变量的作用域并不符合常规。其中一种情况就是你可以在这个变量被声明之前使用它而不会得到报错，对于编程来说这是不好的。
  - 另一方面，`var` 声明的变量只支持全局作用域与函数作用域。
  - `var` 允许在同一个作用域里面重复声明同一名称的变量，但是 `let` 与 `const` 不可以。
- `let` 也可以用来声明一个变量，作用与 `var` 是一致的，但是它没有前者那样的作用域缺陷，因此更推荐使用 `let`
- `const` 用来声明一个常量，常量在被第一次赋值之后就不能改变里面的值，其他属性与 `let` 是一致地。
  - `const` 声明的变量必须在声明的时候赋值。
  - 需要注意的是，对于像数组和对象这样的数据类型，它们存储的是地址，也就是说程序员不能改变一个 const 常量指向的是哪个数组或者对象，但是可以改变这个数组或对象里面的值。
  - `let` 与 `const` 不仅支持全局作用域和局部作用域，还支持块作用域 `{}`，通过 `var` 在块内声明的变量在块之外也是可以访问的，但是通过 `let` 与 `const` 声明的就不可以。

```js
var x = 10;
// 此处 x 为 10
{ 
  var x = 6;
  // 此处 x 为 6
}
// 此处 x 为 6
```

```js
let x = 10;
// 此处 x 为 10
{ 
  let x = 6;
  // 此处 x 为 6
}
// 此处 x 为 10
```

### 标识符命名

- JS 中的变量必须以唯一名称来标识，这样的唯一名称称为标识符。
- 标识符命名规则：
  - 名称可包含字母、数字、下划线和美元符号
  - 名称必须以字母开头
  - 名称也可以 `$` 和 `_` 开头（但是在本教程中我们不会这么做）
  - 名称对大小写敏感（y 和 Y 是不同的变量）
  - 保留字（比如 JavaScript 的关键词）无法用作变量名称

### 数据类型

- 