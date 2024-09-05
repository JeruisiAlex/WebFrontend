## 说明

本文档是一个关于 html5 中支持的常用标签的一个大致介绍，并非包含了所有标签

需要注意的是，html5 是支持自定义标签的，所有的自定义标签都被默认当做行内元素来展开

## 基础标签

- \<!DOCTYPE> 用于定义文档类型，严格来说并不算是一个标签，只是用于告诉浏览器使用的 html 标准版本
  - 标注 html5 版本 \<DOCTYPE html>
- \<html> 定义了 html 文档的开始与结束
  - 应该始终声明 lang 属性来表明文档的语言类型，比如中文网站 \<html lang="zh-cn">
- \<head> 元数据的容器，元数据定义关于 html 文档的数据
  - 以下元素可以放在 \<head> 元素内
    - \<title> 必需，定义了网页的标题
    - \<style> 定义文档的样式信息，这里定义的是内部样式
    - \<base> 用于改变当前文档的相对路径的基准，默认的基准是当前网页的路径。**该标签只能使用一次**
      - 包含 href 与 target 两个属性
    - \<link> 用于链接外部样式或向网站添加图标
      - 常用属性 href, rel, sizes
    - \<meta > 标签定义关于 HTML 文档的元数据，包含4个属性
      - charset：用于定义文档的字符集，通常使用 utf-8
      - name 与 content：用于定义关于网页的一些信息
      - http-equiv：为 content 属性的信息/值提供 HTTP 标头
    - \<script> 定义文档的脚本，可以作为内部脚本，也可以用来引入外部脚本
    - \<noscript> 定义了替代的内容，显示给在浏览器中禁用脚本或浏览器不支持脚本的用户
- \<body> html 文档的内容主体
- \<h1> to \<h6> 标题标签
  - 不要将标题标签仅仅当做字体大小样式改变的标签来使用，因为有的浏览器会使用标题标签来建立索引，标题也有可能被搜索引擎所使用
- \<p> 定义段落
- \<br /> 定义一个简单的换行
- \<hr /> 定义水平线，用于分隔内容
- \<template> 定义用作容纳页面加载时隐藏内容的容器，里面的内容不会被浏览器展示，但是可以通过 js 来获取并展示
  - 在 vue 中这个标签很重要，你会发现每一个 vue 组件最外层都是这个组件



## 文本格式化标签

- \<abbr> 定义缩写词
  - 用 title 属性来标注全称
- \<bdi> 是文本方向与原本标签的方向隔离，官网的描述为标签隔离了一部分文本，这部分文本可能在方向上与外部其他文本不同。当嵌入用户生成的具有未知文本方向的内容时，这个元素是非常有用的
- \<bdo> 定义文本反向
  - 属性 dir，具有 "rtl", "lrt" 两种值
- \<blockquote> 定义长的引用，实际表现为浏览器会为其添加整个段落的缩进
- \<code> 定义一段计算机代码
  - 会删除代码中多余的换行和空白，意味着连续多个的换空白字符会被浏览器自动缩减为一个空白，而换行等字符会在缩减之前被替换为空白字符
- \<del> 为文本添加删除线
- \<dfn> 定义一个术语，可以添加 title 属性，感觉与 abbr 标签类似
- \<em> 将文本变为斜体
- \<ins> 为文本添加下划线
- \<mark> 为文本添加背景颜色，其实可以用 css 调出来，默认黄色背景色，黑色字体
- \<meter> 定义一个仪表盘（其实长得很像进度条，但是官方不推荐当做进度条使用）
  - high：规定范围的高值
  - low：规定范围的低值
  - max：规定范围的最大值
  - min：规定范围的最小值
  - optimum：规定仪表的最佳值
  - value：必需，规定仪表的当前值
- \<pre> 定义预格式化文本，与 \<code> 类似，但是会将原本的文本全部保留
- \<progress> 进度条
  - max：总量
  - value：已完成部分
- \<samp> 定义计算机程序的样本输出
- \<strong> 将文本加粗
- \<sup> 定义上标文本
- \<sub> 定义下标文本
- \<var> 定义编程或数学表达式中的变量。标签内部的内容通常以斜体显示。
- \<wbr> 规定在文本中适合添加换行的位置。当单词太长时，浏览器可能会在错误的位置断开它,可以使用 \<wbr> 元素添加单词断开的机会。

## 表单标签

- \<form> 为接收用户输入创建 html 表单
  - 意在接收用户的格式化数据输入，大多时候会将这些数据传递给服务端
  - 虽然表单自己含有用于发送请求的属性，但是一般并不使用这个属性，在笔者目前接触的项目中，大多采用按钮加方法的方式来发送请求进行提交
  - 该标签可以包含下面的表单元素
- \<input> 定义输入字段，用户可以在其中输入数据
  - 最重要的表单元素，通过 type 属性来设置其样式
  - 除了 type 属性还有很多其他的属性，但是具体的属性用法取决于 type 的值
  - 这是个单标签
  - autofocus 是否自动聚焦
  - disabled 是否禁用
  - placeholder 提示词
  - required 是否必须
  - type 具有下面这些值

| 值                                                           | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [button](https://www.w3school.com.cn/tags/att_input_type_button.asp) | 定义可点击的按钮，主要与 JavaScript 一起使用以激活脚本。html5 中有单独的 button 标签，比这个更实用一些，故不推荐使用该值 |
| [checkbox](https://www.w3school.com.cn/tags/att_input_type_checkbox.asp) | 定义复选框。                                                 |
| [color](https://www.w3school.com.cn/tags/att_input_type_color.asp) | 定义颜色选择器（拾色器）。                                   |
| [date](https://www.w3school.com.cn/tags/att_input_type_date.asp) | 定义日期控件（年月日，无时间）。                             |
| [datetime-local](https://www.w3school.com.cn/tags/att_input_type_datetime-local.asp) | 定义日期和时间控件（年、月、日、时间，无时区）。             |
| [email](https://www.w3school.com.cn/tags/att_input_type_email.asp) | 定义用于输入电子邮件地址的字段。                             |
| [file](https://www.w3school.com.cn/tags/att_input_type_file.asp) | 定义文件选择字段和“浏览”按钮（用于文件上传）。               |
| [hidden](https://www.w3school.com.cn/tags/att_input_type_hidden.asp) | 定义隐藏的输入字段。                                         |
| [image](https://www.w3school.com.cn/tags/att_input_type_image.asp) | 定义图像作为提交按钮。                                       |
| [month](https://www.w3school.com.cn/tags/att_input_type_month.asp) | 定义月份和年份控件（无时区）。                               |
| [number](https://www.w3school.com.cn/tags/att_input_type_number.asp) | 定义用于输入数字的字段。                                     |
| [password](https://www.w3school.com.cn/tags/att_input_type_password.asp) | 定义密码字段。                                               |
| [radio](https://www.w3school.com.cn/tags/att_input_type_radio.asp) | 定义单选按钮。                                               |
| [range](https://www.w3school.com.cn/tags/att_input_type_range.asp) | 定义范围控件（如滑块控件）。                                 |
| [reset](https://www.w3school.com.cn/tags/att_input_type_reset.asp) | 定义重置按钮。                                               |
| [search](https://www.w3school.com.cn/tags/att_input_type_search.asp) | 定义用于输入搜索字符串的文本字段。                           |
| [submit](https://www.w3school.com.cn/tags/att_input_type_submit.asp) | 定义提交按钮。个人感觉意义不大，因为任意按钮绑上点击方法都可以用来提交。 |
| [tel](https://www.w3school.com.cn/tags/att_input_type_tel.asp) | 定义用于输入电话号码的字段。                                 |
| [text](https://www.w3school.com.cn/tags/att_input_type_text.asp) | 默认。定义单行文本字段。                                     |
| [time](https://www.w3school.com.cn/tags/att_input_type_time.asp) | 定义输入时间的控件（无时区）。                               |
| [url](https://www.w3school.com.cn/tags/att_input_type_url.asp) | 定义用于输入 URL 的字段。                                    |
| [week](https://www.w3school.com.cn/tags/att_input_type_week.asp) | 定义周和年控件（无时区）。                                   |

- \<textarea> 定义多行文本输入控件。
  - cols：文本域可见宽度
  - row：文本域可见行数
- \<button> 定义可点击的按钮
  - type：按钮的类型，包括 button，reset 以及 submit 三种值
- \<select> 用于创建下拉列表
  - multiple：用于规定一次是否可以选择多个选项
- \<optgroup> 用于对下拉列表中的选项进行分组
- \<option> 下拉列表中的选项
- \<label> 标签，用来表明需要输入的数据是什么
- \<datalist> 为 input 准备，用于在 input 中添加下拉选项

## 框架标签

- \<iframe> 内联一个网页
  - src：网页来源
  - loading：eager, lazy 两种模式

## 图像标签

- \<img> 在页面中嵌入图片
  - src：图片的地址
  - alt：图片加载失败时的替代文字
- \<map> 与上面的 \<img> 标签以及下面的 \<area> 结合使用，用来标志
- \<area> 与上面的两个标签合用，用于为图片中的一定区域添加特殊用途
- \<canvas> 画布
- \<figcaption> 为图片添加标题
- \<figure> 包裹图片，用于为图片添加标题
- \<picture> 配合 \<source> 使用，用于根据浏览器的尺寸加载不同的图片
- \<svg> 定义 SVG 图形的容易

## 音频/视频标签

- \<audio> 在文档中嵌入声音内容
- \<source> 为媒体元素指定多个媒体资源
- \<track> 为标签 \<audio> 或 \<video> 元素规定文本轨道
- \<video> 在文档中嵌入视频内容

## 链接标签

- \<a> 定义超链接
  - href：规定链接指向的页面 url
  - download：如果链接是一个下载的文件，使用该属性为文件赋予新的名字
- \<link> 定义文档与外部资源的关系，最常用于链接到外部样式表或向网站添加图标
- \<nav> 定义一组导航链接

## 列表标签

- \<menu> 定义无序列表，与 \<ul> 等价
- \<ul> 定义无序列表
- \<ol> 定义有序列表
- \<li> 定义列表项
- \<dl> 定义描述列表
- \<dt>  定义描述列表中的术语/名称
- \<dd> 定义描述列表中术语的描述/值

## 表格标签

- \<table> 定义表格
- \<caption> 定义表格标题
- \<th> 定义表格中的表头单元格
- \<tr> 定义表格中的行
- \<td> 定义表格中的单元
- \<thead> 定义表格中的表头内容
- \<tbody> 定义表格中的主体内容
- \<tfoot> 定义表格中的表注内容
- \<col> 规定 \<colgroup> 中每列的属性
- \<colgroup> 规定表格中供格式化的列组

## 样式和语义标签

- \<div> 一个块级的盒子，最常用的标签
- \<span> 一个行内元素的盒子，用的比较少
