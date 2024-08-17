# HTML5

如果有人不幸看到了这个仓库，并想全面学习一下 Web 前端开发，请注意以下几点：

1. 首先作者很菜，技术水平比较有限。
2. 其次这个仓库是作者在系统性回顾的时候写的，会不定期地修改里面表述与理解的错误。
3. 最后如果你还是想看的话，记得最好自己了解一下 Web 标准以及不同常见浏览器之间的区别（主要是内核）



一些可以查阅的文档网址：

推荐地址：http://www.w3school.com.cn/

https://developer.mozilla.org/zh-CN/



## 关于标签

### 标签的分类

- 标签分为**单标签**和**双标签**。

  - **单标签**：极少使用

  ```html
  <img />
  ```

  - **双标签**：大规模使用

  ```html
  <div>	</div>
  ```

### 标签之间的关系

- 标签的关系分为两种：**包含关系**与**并列关系**

#### 包含关系

- 简单来说就是一个标签被包含在另一个标签里面，类似于父子关系。
- 显然，只有双标签才能包含其他的标签。

#### 并列关系

- 两个标签处于同级关系，类似于兄弟关系。

## 常见的基础标签

### 骨架标签

```html
<html> 网页的根标签，需要写在最外面 </html>
<head> 网页的头部 </head>
<title> 网页的标题 </title>
<body> 网页的主体，网页内容基本都在这里面 </body>
```

### 设置用的标签

```html
<!DOCTYPE> 声明文档的类型，需要写在最外面
<meta charset = "UTF-8"> 在 head 里面表明文件的字符集
```

### 文本格式化标签

```html
<h1></h1> 标题标签，有 h1 到 h6，独占一行
<p></p> 段落标签，段落之间有空隙
<br /> 强制将一段文字进行换行，换行不会产生空隙
<strong></strong> <b></b> 加粗文字的标签
<em></em> <i></i> 倾斜文字的标签
<dei></dei> <s></s> 给文字添加删除线的标签
<ins></ins> <u></u> 给文字添加下划线的标签
```

### 盒子标签

```html
<div>
	独占一行
</div>
<span>
	
</span>
```

### 图像标签

```html
<img src="图像路径" alt="替代文字" title="标题，鼠标放上去显示"/>

img 属性
width: 宽度，单位 px
height: 高度，单位 px
border: 边框粗细，单位 px
```

### 链接标签

```html
<a href="跳转路径" target="目标窗口的跳转方式"></a>

a 属性
target: _self为默认值在当前窗口打开，_blank在新窗口打开
href: # 代表空连接；如果地址是一个文件，那么会直接下载这个文件；#+id 跳转至有对应 id 的标签
```

### 表格标签

```html
<table> 定义表格的标签
    <thead> 表格的头部区域
        <tr> 表格中的一行
        	<th> 表头中的一格 </th>
        	<th> 表头中的一格 </th>
            ···
    	</tr>
    </thead>
    <tbody> 表格的主体区域
        <tr> 表格中的一行
        	<td> 表格中的每一格</td>
        	<td> 表格中的每一格</td>
            ···
    	</tr>
    </tbody>
</table>

table 属性：
align: left, center, right，规定表格相对周围元素的对齐方式
border: 1或""，默认为""，表示没有边框
cellpadding: 单元边沿与其内容之间的空白，默认值1像素
cellspacing: 单元格之间的空白，默认值2像素
width: 表格的宽度，百分比或像素
height: 表格的宽度，百分比或像素

td 属性：
rowspan：跨行合并单元格
colspan：跨列合并单元格
```

### 列表标签

#### 无需列表

```html
<ul>
    <li></li>
    <li></li>
    ···
</ul>
```

#### 有序列表

```html
<ol>
    <li></li>
    <li></li>
    ···
</ol>
```

#### 自定义列表

```html
<dl>
    <dt> 名词1 </dt>
    <dd> 名词1解释1 </dd>
    <dd> 名词1解释2 </dd>
    ···
</dl>
```

### 表单标签

#### 表单域

```html
<form> 表单域
    
</form>

form 属性：
action: 表单提交的 url 地址
method: 提交的方法
name: 表单的名称
```

#### 表单元素

```html
<input />

input 属性： 
type: 最终要的属性，定义input的类型，button, checkbox, file, hidden, image, password, radio, reset, submit, text
name: input 元素的名称
value: input 元素的值
checked: 使 input 元素首次加载时应当被选中，主要用于单选框和复选框
maxlength: 规定输入字段中的字符的最大长度，主要用于 text, password 这种输入字符串的内容

<label for="绑定标签的 id"></label>

<select>
    <option> 选项1 </option>
    <option> 选项2 </option>
    ···
</select>

option 属性:
selected: selected，表示被选中

<textarea>

</textarea>

textarea 属性：
col: 每行中的字符数
rows：显示的行数
```

