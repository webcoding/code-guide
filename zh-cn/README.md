# HTML and CSS code guide
开发灵活，耐用，可持续的HTML和CSS标准。



----------



## 目录

* [黄金法则](#golden-rule)
* [HTML](#html)
  * [语法](#html-syntax)
  * [HTML5 doctype](#html5-doctype)
  * [实用而非语义](#pragmatism-over-semantics)
  * [属性顺序](#attribute-order)
  * [JavaScript generated markup](#javascript-generated markup)
* [CSS](#css)
  * [CSS syntax](#css-syntax)
  * [Declaration order](#declaration-order)
  * [Formatting exceptions](#formatting-exceptions)
    * [Prefixed properties](#prefixed-properties)
    * [Rules with single declarations](#rules-with-single-declarations)
  * [Human readable](#human-readable)
    * [Comments](#comments)
    * [Classes](#classes)
    * [Selectors](#selectors)
  * [Organization](#organization)
* [Writing copy](#copy)
  * [Sentence case](#sentence-case)



----------


# 代码书写指南

参考摘自 [file an issue on GitHub](https://github.com/mdo/code-guide)，有改动。

## 黄金法则

> 任何代码库中的所有代码应该看起来像是一个人书写的，不管有多少人贡献过代码。

这意味着任何时候都要严格执行这些商定的准则。对于增加或减少代码的法则，请参看 [Code-guide](https://github.com/webcoding/code-guide/tree/master/zh-cn).

----------

## HTML


### HTML 语法

* 使用两个空格的 soft-tabs
* 应每层嵌套元素缩进一次（2个空格）
* 请务必实用双引号，而非单引号
* 不要自闭元素包括一个斜线

**错误示例：**

````html
<!DOCTYPE html>
<html>
<head>
<title>Page title</title>
</head>
<body>
<img src='images/company-logo.png' alt='Company' />
<h1 class='hello-world'>Hello, world!</h1>
</body>
</html>
````

**正确示例：**

````html
<!DOCTYPE html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <img src="images/company-logo.png" alt="Company">
    <h1 class="hello-world">Hello, world!</h1>
  </body>
</html>
````


### HTML5 doctype

在每个浏览器可以用这个简单的DOCTYPE，故在每个HTML页面开始强制执行的标准模式。

````html
<!DOCTYPE html>
````


### 实用大于语义

努力保持HTML的标准和语义，但不要牺牲实用性。用最少的复杂度尽可能少的标签实现需求。

### 属性顺序

HTML 属性应该遵循特定的顺序，以便能更易阅读代码。

* class
* id
* data-*
* for|type|href

比如你的代码看起来应该像这样:

````html
<a class="" id="" data-modal="" href="">链接示例</a>
````

### JavaScript 生成标记

使用JavaScript生成标记，会使内容更难找到，更难编辑且性能更低。切记不要这样做。



----------



## CSS

### 外部CSS引用

必须使用如下格式(rel在前，href在后，无type="text/css"及charset)：

````
&lt;link rel="stylesheet" href="css_example_url" &gt;
````

### CSS 注意事项

* 无特殊说明，编码统一为utf-8；
* 防止文件合并及编码转换时造成问题，请将样式中文字体名字改成对应的英文名字（unicode码），如：宋体（ \5b8b\4f53）微软雅黑（”Microsoft YaHei”,”\5FAE\8F6F\96C5\9ED1″）；
* 书写代码前，考虑并提高样式重复使用率；
* 禁止使用 `expression` 表达式；
* 禁止滥用 `！important`；
* 能缩写的尽量缩写，如 `padding:5px 0 0 5px;`；
* 层级(z-index)必须清晰明确，适当划分组件层级范围，禁止层级间盲目攀比；
* 为方便组件模块化和提高弹性，正常情况下，为避免外边界冲突，组件不应设置外边界，外边界用组合css方式实现，如：m10{margin:10px}mt10{margin-top:10px}等；
* 必须为大区块&重要模块的样式添加注释，小区块适量注释；
* 正式发布前应进行压缩，压缩后文件的命名应添加”.min”后缀；
* 代码缩进与格式：请参照以下 CSS 书写规范；

### CSS 书写规范

* 使用四个空格的 soft-tabs 缩进
* 写组选择器时，保持选择器各占一行
* 在属性块的左 “{” 前应该有一个空格
* 关闭属性块的右 “}” 要新起一行
* 每个属性的 “:” 后包含一个空格
* 每个属性应该自己独占一行
* 分割选择器的 “,” 后应该包含一个空格
* Don't include spaces after commas in RGB or RGBa colors, and don't preface values with a leading zero
* 小写所有16进制值, 例如, `#fff` 而非 `#FFF`
* 使用简写16进制值, 例如, `#fff` 而非 `#ffffff`
* 选择器中引用属性值, 例如, `input[type="text"]`
* 避免0值设置单位, 例如, `margin: 0;` 而非 `margin: 0px;`

**错误示例：**

````css
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}
````

**正确示例：**

````css
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin: 0 0 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
````

常见的CSS术语，请参见 [syntax section of the Cascading Style Sheets article](http://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax) on Wikipedia.


### 属性顺序

相关属性应放在一起，将定位与盒模型属性写在最前面，其次是排版和视觉效果的属性。

````css
.declaration-order {
  /* Positioning 定位 */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model 盒模型 */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography 排版 */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5
  color: #333;
  text-align: center;

  /* Visual 视觉 */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc 其他 */
  opacity: 1;
}
````

关于属性顺序的完整列表，请参考 [Recess](http://twitter.github.com/recess).


### 格式化例外

某些情况下，这是有道理的，稍微偏离默认的 [语法](#css-syntax).

#### 前缀属性

当使用供应商前缀的属性时，每个属性缩进到vlaue值垂直对齐的位置，方便多行编辑。

````css
/* Corner radius-圆角 */
.selector {
  -webkit-border-radius: 3px;
     -moz-border-radius: 3px;
          border-radius: 3px;
}
````
注：`-khtml-border-radius: 3px;` 是苹果的那个浏览器的，现在使用 `-webkit-`

在 Textmate、Sublime Text 2 以及 notepad++等工具中, 都支持多行编辑。

In Textmate, use **Text &rarr; Edit Each Line in Selection** (&#8963;&#8984;A). In Sublime Text 2, use **Selection &rarr; Add Previous Line** (&#8963;&#8679;&uarr;) and **Selection &rarr;  Add Next Line** (&#8963;&#8679;&darr;).

#### 单一属性的书写规则

在有些情况下，每个样式只有一个属性，考虑到可读性及更快地编辑删除等，保持同一行书写。

````css
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

.sprite {
  display: inline-block;
  width: 16px;
  height: 15px;
  background-image: url(../img/sprite.png);
}
.icon           { background-position: 0 0; }
.icon-home      { background-position: 0 -20px; }
.icon-account   { background-position: 0 -40px; }
````


### 可读性

代码是由人来书写和维护的。确保你的代码有很好的注释描述，以便他人使用。

#### 注释

好的代码都有一个良好的代码注释而不仅仅是一个类名

**Bad example:**

````css
/* Modal header */
.modal-header {
  ...
}
````

**Good example:**

````css
/* Wrapping element for .modal-title and .modal-close */
.modal-header {
  ...
}
````

#### 类名与命名

* 保持类名使用小写字母或连接符 (不要使用下划线或驼峰命名法)
* 避免使用随意的首字符命名法
* 保持命名尽可能短并简洁
* 使用有意义的命名；使用结构化或目的性的意义名称
* 根据最近的父组件基类作为命名前缀
* 为JavaScript预留钩子的命名，请以 JS_ 起始，比如：JS_ui-tab, JS_slidebox；或者使用 data-* 挂钩JS功能

**Bad example:**

````css
.t { ... }
.red { ... }
.header { ... }
````

**Good example:**

````css
.tweet { ... }
.important { ... }
.tweet-header { ... }
````

#### 选择器

* 在通用的元素标签中使用类
* 要保持尽量简短，并限制每个选择器最多三个class
* 必要时使用最近的父类 (如，在不使用前缀类时)

**Bad example:**

````css
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }
````

**Good example:**

````css
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
````

### 组织

* 组织代码段的组成部分
* 指定一个一致的注释层次结构
* 如果使用多个css文件，则按组件进行划分



----------



## 复制

### Sentence case

务必写文案，包括标题和代码注释，in [sentence case](http://en.wikipedia.org/wiki/Letter_case#Usage). 换句话说，除了标题和专有名词，只有第一个字应予以资本化。



----------



### Thanks

Heavily inspired by [Idiomatic CSS](https://github.com/necolas/idiomatic-css) and the [GitHub Styleguide](http://github.com/styleguide). Made with all the love in the world by [@mdo](http://twitter.com/mdo).

