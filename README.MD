# 前端开发规范
代码是写给人看的，而不是给计算机读的~

拒做“我栽树后人填坑”

## 文件命名规则
采用驼峰式命名法，首单词全部小写，之后每个单词头字母大写，

例：`myProjectName`

## HTML

### 语法
- 使用soft tab（4个空格）
- 嵌套节点应该缩进
- 在属性上，使用双引号，而非单引号
- 属性名全小写，用`-`做份分隔符
- 不要在自动闭合标签结尾处使用斜线
- 不要忽略可选的关闭标签，例如`<div></div>`、`<span></span>`等
```
<!DOCTYPE html>
<html>
    <head>
        <title></title>
    </head>
    <body>
        <img src="" alt="">

        <h1 class="h1-name">Hello, world!</h1>
    </body>
</html>
```

### HTML5 doctype
在页面开发使用这个简单的`doctype`来启用标准模式，使其在每个浏览器尽可能一致的展现
虽然`doctype`不区分大小写，但是按照管理，`doctype`大写
```
<!DOCTYPE html>
<html>
	...
</html>
```

### lang属性
根据HTML5规范，应在`html`标签加上`lang`属性，这才能给语音/翻译工具带来正确的识别


[点击详解关于`lang`属性的说明](http://w3c.github.io/html/semantics.html#the-html-element)

[点击前往微软查询关于信息](https://msdn.microsoft.com/en-us/library/ms533052(v=vs.85).aspx)

例如常用语言列表，如中文：`zh-cn`，香港：`zh-hk`, 台湾：`zh-tw`

```
<!DOCTYPE html>
<html lang="zh-cn">
	...
</html>
```

### 字符编码
通过声明一个明确的字符编码，让浏览器轻松、快速的确定适合网页内容的渲染方式，通常指定为`UTF-8`
```
<!DOCTYPE html>
<html lang="zh-cn">
    <head>
        <meta charset="UTF-8">
    </head>
	...
</html>
```

### 引入CSS, JS
根据HTML5规范, 通常在引入CSS和JS时不需要指明 type，因为`text/css`和`text/javascript`分别是他们的默认值

HTML5 规范链接：

[link规范](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)

[style规范](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element)

[script规范](https://www.w3.org/TR/2011/WD-html5-20110525/scripting-1.html#the-script-element)
```
<!-- 引入css -->
<link rel="stylesheet" href="code_guide.css">

<style>
    ...
</style>

<!-- 引入js -->
<script src="xxx.js"></script>

<script>
    ...
</script>
```


### 属性顺序
属性应该按照特定的顺序出现以保证易读性
- `class`
- `id`
- `name`
- `data-*`
- `src`、`for`、`type`、`href`、`value`、`max-length`、`max`、`min`、`pattern`
- `placeholder`、`title`、`alt`
- `aria-*`、`role`
- `required`、`readonly`、`disabled`

class是为高可复用组件设计的，所以应处在第一位

id更加具体且应该尽量少使用，所以将它放在第二位

```
<a class="" id="" data-modal="toggle" href=""></a>

<input class="" type="text">

<img src="" alt="">
```

### boolean属性
boolean属性指不需要声明取值的属性，XHTML需要每个属性声明取值，但是HTML5并不需要;boolean属性的存在表示取值为true，不存在则表示取值为false

[点击前去详解](https://html.spec.whatwg.org/multipage/common-microsyntaxes.html#boolean-attributes)

```
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
    <option value="1" selected>1</option>
</select>
```

### JS生成标签
尽量避免在JS文件中生成标签，会让内容变得更难查找，更难编辑，性能更差

### 减少标签数量
在编写HTML代码时，需要尽量避免多余的父节点；很多时候，需要通过迭代和重构来使HTML变得更少

```
<!-- 不良写法，造成多余父节点 -->
<span class="avatar">
    <img src="...">
</span>

<!-- 最优写法 -->
<img class="avatar" src="...">
```

### 实用高于完美
尽量遵循HTML标准和语义，但是不应该以浪费实用性作为代价；

任何时候都要用尽量小的复杂度和尽量少的标签来解决问题。


## CSS

### 命名
类名使用小写字母，以`-`分隔，如：`header-logo`

id采用驼峰式命名，如：`header`、`headerLogo`

### 缩进
使用soft tab（4个空格）

```
#div {
    position: absolute;
    top: 10px;
    left: 10px;

    border-radius: 10px;
    width: 50px;
    height: 50px;
}
```

### 分号
每个属性声明末尾都要加分号
```
.element {
    width: 20px;
    height: 20px;

    background-color: red;
}
```

### 空格
以下几种情况不需要空格：
- 属性名后
- 多个规则的分隔符','前
- `!important`的`!`后面
- 属性值中`(`后和`)`前
- 行末不要有多余的空格
```
/* 不良规范 */
.element {
    color :red! important;
    background-color: rgba(0,0,0,.5);
}

/* 良好规范 */
.element {
    color: red !important;
    background-color: rgba(0, 0, 0, .5);
}
```

以下几种情况需要空格：
- 属性值前
- 选择器`>`, `+`, `~`前后
- `{`前
- `!important`的`!`前面
- `@else` 前后
- 属性值中的`,`后
- 注释`/*`后和`*/`前
```
/* 不良规范 */
.element ,
.dialog{
    ...
}

/* 良好规范 */
.element,
.dialog {

}

/* 不良规范 */
.element>.dialog{
.dialog{
    ...
}

/* 良好规范 */
.element> .dialog{

}

/* 不良规范 */
.element{
.dialog{
    ...
}

/* 良好规范 */
.element {

}
```

### 空行
以下几种情况需要空行：

- 文件最后保留一个空行
- `}`后最好跟一个空行，包括scss中嵌套的规则
- 属性之间需要适当的空行，具体见属性声明顺序

```
/* 不良规范 */
.element {
    ...
}
.dialog {
    color: red;
    &:after {
        ...
    }
}

/* 良好规范 */
.element {
    ...
}

.dialog {
    color: red;

    &:after {
        ...
    }
}
```

### 换行
以下几种情况不需要换行：

- `{`前
```
/* 不良规范 */
.element
{...}

/* 良好规范 */
.element {
    ...
}
```

以下几种情况需要换行：

- `{`后和`}`前
- 每个属性独占一行
- 多个规则的分隔符`,`后

```
/* 不良规范 */
.element, .dialog {
    ...
}

/* 良好规范 */
.element,
.dialog {
    ...
}
```

### 注释
注释统一用`/* */`（scss中也不要用`//`，因为在编译的时候，会忽略此注释），具体参照右边的写法；

缩进与下一行代码保持一致；

可位于一个代码行的末尾，与代码间隔一个空格。
```
/* 模态框头部 */
.modal-header {
    ...
}

/*
 * 模态框头部
 */
.modal-header {
    ...
}

.modal-header {
    /* 50px */
    width: 50px;

    color: red; /* color red */
}
```

### 引号
最外层统一使用双引号；

`url`的内容要用引号；

属性选择器中的属性值需要引号

```
.element:after {
    content: "";
    background-image: url("");
}

li[data-id="xxx"] {
    ...
}
```

### 属性声明顺序
相关的属性声明按右边的顺序做分组处理，组之间需要有一个空行
- 影响文档流的属性，如：`display`, `position`, `float`, `clear`, `visibility`, `table-layout`等
- 自身盒模型的属性，如：`width`, ` height`, `margin`, `padding`, `border`等
- 排版相关属性，如：`font`, `line-height`, `text-align`, `text-indent`, `vertical-align`等
- 装饰性属性，如：`color`, `background`, `opacity`, `cursor`等
- 生成内容的属性，或其他属性，如：`content`, `list-style`等

```
.element {
    display: block;
    position: relative;
    float: left;
    
    width: 100px;
    height: 100px;
    
    background: red;
}
```

### 颜色
颜色16进制用小写字母；

颜色16进制尽量用简写

```
/* 不良规范 */
.element {
    color: #ABCDEF;
    background-color: #001122;
}

/* 良好规范 */
.element {
    color: #abcdef;
    background-color: #012;
}
```


### 属性简写
属性简写需要你非常清楚属性值的正确顺序，而且在大多数情况下并不需要设置属性简写中包含的所有值，所以建议尽量分开声明会更加清晰
```
/* 不良规范 */
.element {
    transition: opacity 1s linear 2s;
}

/* 良好规范 */
.element {
    transition-delay: 2s;
    transition-timing-function: linear;
    transition-duration: 1s;
    transition-property: opacity;
}
```

### 媒体查询
尽量将媒体查询的规则靠近与他们相关的规则，不要将他们一起放到一个独立的样式文件中，或者丢在文档的最底部，这样做只会让大家以后更容易忘记他们
```
.element {
    ...
}

@media (max-width: 1280px) {
    .element {
        ...
    }
}
```


### 其他
- 不允许有空的规则

- 元素选择器用小写字母

- 去掉小数点前面的0

- 去掉数字中不必要的小数点和末尾的0

- 属性值'0'后面不要加单位

- 同个属性不同前缀的写法需要在垂直方向保持对齐，具体参照右边的写法

- 无前缀的标准属性应该写在有前缀的属性后面

- 不要在同个规则里出现重复的属性，如果重复的属性是连续的则没关系

- 不要在一个文件里出现两个相同的规则

- 用 border: 0; 代替 border: none;

- 选择器不要超过4层（在scss中如果超过4层应该考虑用嵌套的方式来写）

- 发布的代码中不要有 @import

- 尽量少用'*'选择器


## Javascript

### 缩进

使用soft tab（4个空格）

### 分号
以下几种情况后需加分号：

- 变量声明
```
let obj = {};
```

- 表达式
```
x++;
```

- return
```
let callback = () => {
    return 123;
};
```
- throw
```
try {
   throw n;
} catch (e) {
   if (e <= 50) {
   } else {
      throw e;
   }
}
```

- break
```
for (let i = 10; i > 0; i --) {
    if (i == 5) {
        break;
    }
    console.log(i);
}
```
- continue
```
let i = 0;
let n = 0;

while (i < 5) {
  i++;

  if (i === 3) {
    continue;
  }

  n += i;
}
```

- do-while
```
do {
    x++;
} while (x < 10);
```

### 空格
以下几种情况不需要空格：
- 对象的属性名后
```
let obj = {
  o: 1,  
};
```

- 前缀一元运算符后
- 后缀一元运算符前
```
++x;
y++;
z = x ? 1 : 2;
```

- 函数调用括号前
- 无论是函数声明还是函数表达式，`(`前不要空格
```
let fn = function(arg) {
    return arg;
}

fn(123);
```

- 数组的`[`后和`]`前
```
let arr = [1, 2];
```

- 对象的`{`后和`}`前
```
let obj = {a: 1, b: 2};
```

- 运算符'('后和')'前
```
let a = (1 + 2) * 3;
```

以下几种情况需要空格：
- 二元运算符前后
- 三元运算符'?:'前后
```
1 ? true : false;
```

- 代码块`{`或`}`
    - 如：`else`, `while`, `catch`, `finally`之前
    - 如：`if`, `else`, `for`, `while`, `do`, `switch`, `case`, `try`, `catch`, `finally`, `with`, `return`, `typeof`之后 
```
for (let i = 0; i < 6; i++) {
    x++;
}

if (true) {
    
} else {
    
}
```

- 单行注释`//`后（若单行注释和代码同行，则`//`前也需要），多行注释`*`后
```
// 单行注释

/*
* 多行注释
*/
```

- 对象的属性值前
```
let obj = {
  a: 1,  
};
```

- for循环，分号后留有一个空格，前置条件如果有多个，逗号后留一个空格
```
for (let i = 0; i < 6; i++) {
}
```

- 无论是函数声明还是函数表达式，`{`前一定要有空格
```
let fn = () => {};
```

- 函数的参数之间
```
let fn = (arr, obj, bool) => {};
```

### 空行
以下几种情况需要空行：
- 变量声明后（当变量声明在代码块的最后一行时，则无需空行）
```
let fn;

fn = () => 2;
```

- 注释前（当注释在代码块的第一行时，则无需空行）
```
// 这是一行注释
let a;
```

- 代码块后（在函数调用、数组、对象中则无需空行）
```
// 定义变量
let fn;

// 赋值变量
fn = (arg) => arg;

// 调用
fn(1);
```

- 文件最后保留一个空行
 
### 换行
换行的地方，行末必须有`,`或者运算符；

以下几种情况不需要换行：

- 下列关键字后：`else`, `catch`, `finally`
- 代码块`{`前
```
if () {
    ...
} else {
    ...
}

try {
    ...
} catch (e) {
    ...
} finally {
    ...
}
```


以下几种情况需要换行：
- 代码块`{`后和`}`前
- 变量赋值后
```
let obj = {
    b: 1,
    c: 2
};

if () {
    ...
}
```

### 单行注释
双斜线后，必须跟一个空格；

缩进与下一行代码保持一致；

可位于一个代码行的末尾，与代码间隔一个空格
```
if (true) {
    // 如果为true，返回1
    return 1;
}

let obj = {}; // 定义空变量
```

### 多行注释
最少三行, `*`后跟一个空格，具体参照右边的写法；

建议在以下情况下使用：

- 难于理解的代码段
- 可能存在错误的代码段
- 浏览器特殊的HACK代码
- 业务逻辑强相关的代码
```
/*
* 这是多行注释
*/
```

### 文档注释
各类标签`@param`, `@method`等请参考[usejsdoc](http://usejsdoc.org/)和[JSDoc Guide](http://yuri4ever.github.io/jsdoc/)

建议在以下情况下使用：
- 所有常量
- 所有函数
- 所有类
```
/**
 * @foo
 * @desc 一个带参数的函数
 * @param {string} a - 参数a
 * @param {number} b=1 - 参数b默认值为1
 * @param {string} c=1 - 参数c有两种支持的取值</br>1—表示x</br>2—表示xx
 * @param {object} d - 参数d为一个对象
 * @param {string} d.e - 参数d的e属性
 * @param {string} d.f - 参数d的f属性
 * @param {object[]} g - 参数g为一个对象数组
 * @param {string} g.h - 参数g数组中一项的h属性
 * @param {string} g.i - 参数g数组中一项的i属性
 * @param {string} [j] - 参数j是一个可选参数
 */
function foo(a, b, c, d, g, j) {
    ...
}
```

### 引号
最外层统一使用单引号
```
let str = '<div class="div"></div>';
```

### 变量命名
- 标准变量采用驼峰式命名（除了对象的属性外，主要是考虑到cgi返回的数据）
```
let myName = "xxx";
```

- 常量全大写，用下划线连接
```
const USER_NAME = "xxx";
```

- `ID`在变量名中全大写
```
let userID = 1;
```

- 'URL'在变量名中全大写
```
let shareURL = "";
```

- 'Android'在变量名中大写第一个字母
```
let AndroidVersion;
```

- 'iOS'在变量名中小写第一个，大写后两个字母
```
let iOSVersion;
```

- 构造函数，大写第一个字母
```
function Person(name) {
    this.name = name;
}
```

- jquery对象必须以`$`开头命名
```
let $body = $('body');
```

### 变量声明
一个函数作用域中所有的变量声明尽量提到函数首部，用一个`let`声明，不允许出现两个连续的`let`声明
```
let a = 1,
    b = 2,
    c = 3;
```

### 函数
无论是函数声明还是函数表达式，'('前不要空格，但'{'前一定要有空格，如果是使用箭头函数，'('前需要空格
```
let fn = function() {};

// 箭头函数
let fn2 = () => {}; 
```

函数调用括号前不需要空格
```
// 箭头函数
let fn2 = () => {}; 

fn2();
```

不要给inline function命名
```
// 不良规范
let a = [1, 2, function a() {
    ...
}];

// 良好规范
let a = [1, 2, function() {
    ...
}];
```

参数之间用`, `分隔，注意逗号后有一个空格
```
let fn = (a, b, b) => a + b + c;

fn(1, 2, 3);
```

### 数组、对象
对象属性名不需要加引号；

对象以缩进的形式书写，不要写在一行；

数组、对象最后不要有逗号
```
// 不良规范
let a = {
    'b': 1
};

let a = {b: 1};

let a = {
    b: 1,
    c: 2,
};

// 良好规范
let a = {
    b: 1,
    c: 2
};
```

### 括号
下列关键字后必须有大括号（即使代码块的内容只有一行）：`if`, `else`, `for`, `while`, `do`, `switch`, `try`, `catch`, `finally`, `with`

```
// 不良规范 
if (condition)
    doSomething();

// 良好规范
if (condition) {
    doSomething();
}
```

### null

适用场景：
- 初始化一个将来可能被赋值为对象的变量
- 与已经初始化的变量做比较
- 作为一个参数为对象的函数的调用传参
- 作为一个返回对象的函数的返回值

不适用场景：
- 不要用null来判断函数调用时有无传参
- 不要与未初始化的变量做比较

```
// 不良规范
function test(a, b) {
    if (b === null) {
        ...
    }
}

let a;

if (a === null) {
    ...
}

// 良好规范
let a = null;

if (a === null) {
    ...
}
```

### undefined
永远不要直接使用`undefined`进行变量判断

使用`typeof`和字符串`undefined`对变量进行判断
```
// 不良规范
if (person === undefined) {
    ...
}

// 良好规范
if (typeof person === 'undefined') {
    ...
}   
```

### 其他
不要混用tab和space

对上下文this的引用只能使用`_this`, `that`, `self`其中一个来命名
```
let fn = function() {
    let _this = this;
    
    // 或
    let that = this;
    
    // 或
    let self = this;
}
```

`switch`的`case`和`default`一定要有注释特别说明

```
switch (condition) {
    // ...
    case 1:
    
    // ...
    case 2:
        ...
        break;
        
    // 默认情况下
    default: 
}
```