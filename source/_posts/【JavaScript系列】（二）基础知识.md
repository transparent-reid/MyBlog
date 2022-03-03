---
title: 【JavaScript系列】（二）基础知识
date: 2022-03-03 11:30:39
tags:
  - JavaScript
  - 编程语言
  - 前端
categories: 计算机
---

# JavaScript 基础知识

> 本章内容主要是对 JavaScript 的基本语法进行一个梳理和概述，所以尽量用最简单的语言来总结出一些关键知识点。如果想要了解得更加详细，可以去[现代 JavaScript 教程](https://zh.javascript.info/)中访问自己想要了解的内容。

## 在 HTML 文档中插入 JavaScript

我们几乎可以在 HTML 文档的任意地方插入 JavaScript 程序，在标签`<script>`的帮助下。
例如：

```html
<!DOCTYPE html>
<html>
  <body>
    <p>script 标签之前...</p>

    <script>
      alert("Hello, world!");
    </script>

    <p>...script 标签之后</p>
  </body>
</html>
```

当浏览器遇到`<script>`标签时，代码会自动运行。

`<script>`标签中会用到一些特性，当然这些特性现在很少用了。
比如`type`特性：`<script type=...>`
再比如`language`特性：`<script language=...>`

如果这个网站的 JavaScript 代码量很大，放在 HTML 文档中显然不是一个好主意，所以我们也可以通过**外部脚本**的方式，将 JavaScript 代码放在另一个文件中，然后通过`src`特性添加到 HTML 文件中。

```javascript
<script src="/path/to/script.js"><script>
```

## 代码结构

### 语句

语句是执行行为的语法结构和命令。
语句之间可以用分号进行分割。

### 分号

当存在换行符时，在大多数情况下可以省略分号。
比如下面的代码也是可以运行的：

```javascript
alert("Hello");
alert("World");
```

但是有些情况下不写分号会出现一些意想不到的奇怪错误，所以个人建议还是把分号加上吧。

### 注释

单行注释以两个正斜杠`//`开始。

```javascript
//这是一条注释
alert("Hello");
```

多行注释以一个正斜杠和星号开始`/*`并以一个星号和正斜杠结束`*/`。

```javascript
/*这是一条
多行
注释*/
alert("Hello");
```

> 注意：不支持嵌套注释。

## 变量

**变量**是数据的“命名存储”。我们可以使用变量来保存各种信息。
在 JavaScript 中创建一个变量需要用到`let`关键字。
创建了一个变量之后，就可以使用赋值运算符`=`为变量添加一些数据。

```javascript
let message;
message = "Hello";
```

当然这两条语句也可以简洁化为一条语句：

```javascript
let message = "Hello";
```

JavaScript 的变量命名有两个限制：

- 变量名必须仅包含字母、数字、符号`$`和`_`。
- 首字母必须非数字。

> 区分大小写
> 允许非英文字母，但不推荐

有变量的声明，那么肯定有常量的声明。
声明一个常熟变量，可以使用`const`而非`let`：

```javascript
const myBirthDay = "...";
```

使用`const`声明的变量称为“常量”，它们不能被修改，如果你尝试修改就会发现报错。

一个普遍的做法是将常量用作别名，以便记住那些在执行之前就已知的难以记住的值。
使用*大写字母*和*下划线*来命名这些常量。
但是如果这个常数是在运行期间得到的，而不是在运行之前就赋值的，那么这个常数还是采用一般变量的命名法命名：

```javascript
const pageLoadTime = /*网页 加载时间*/
```

## 数据类型

在 JavaScript 中有 8 种基本的数据类型（7 种原始类型和一种引用类型）。

### Number 类型

number 类型代表整数和浮点数。
数字可以有很多操作，比如加减乘除等。
除了常规的数字，还包括所谓的“特殊数值”也属于这种类型：`Infinity`、`-Infinity`、`NaN`。

- `Infinity`代表数学概念种的无穷大（∞）。
- `NaN`代表一个计算错误。它是一个不正确的或者一个未定义的数学操作所得到的结果。`NaN`是粘性的，任何对`NaN`的进一步数学运算都会返回`NaN`。
  > 有一个例外：`NaN ** 0`的结果为 1。

### BigInt 类型

在 JavaScript 中，number 类型无法表示大于（$2^{53}-1$），或小于$-(2^{53}-1$)的整数，由于技术限制。
`BigInt`类型是最近被添加到 JavaScript 语言中的，用于表示任意长度的**整数**。
可以通过将`n`附加到整数字段的末尾来创建`BigInt`值。

```javascript
const bigInt = 1234567890123456789012345678901234567890n;
```

### String 类型

JavaScript 中的字符串必须被括在括号里。

```javascript
let str = "Hello";
let str2 = "Single quotes are ok too";
let phrase = `can embed another ${str}`;
```

在 JavaScript 中，有三种包含字符串的方式。

1. 双引号
2. 单引号
3. 反引号

其中双引号和单引号都是简单引用，没什么差别。
反引号是**功能扩展**引号。它们允许我们通过将变量和表达式包装在`${...}`中，来将它们嵌入到字符串中。

> JavaScript 中没有 char 类型。

### Boolean 类型

boolean 类型仅包含两个值：`true`和`false`。
这个跟其他语言类似，没啥好说的。

### null 值

特殊的`null`值不属于上述任何一种类型。
JavaScript 中的`null`不代表不存在的 object 或者 null 指针，仅仅代表一个“无”的特殊值，表示未知。

### undefined 值

特殊值`undefined`和`null`一样自成类型。
如果一个变量已被声明，但未被赋值，那么它的值就是`undefined`。
当然也可以显式地将`undefined`赋值给变量。但是不建议这样做，通常这种情况会将一个`null`写入变量中，而`undefined`则保留作为未进行初始化的事物的默认初始值。

### object 类型和 symbol 类型

`object`类型是一个特殊的类型。
其他所有数据类型都被称为“原始类型”，因为它们的值只包含一个单独的内容。相反，`object`则用于储存数据集合和更复杂的实体。
`symbol`类型用于创建对象的唯一标识符。

### typeof 运算符

`typeof`运算符返回参数的类型。
对`typeof x`的调用会以字符串的形式返回数据类型：

```javascript
typeof undefined; // "undefined"

typeof 0; // "number"

typeof 10n; // "bigint"

typeof true; // "boolean"

typeof "foo"; // "string"

typeof Symbol("id"); // "symbol"

typeof Math; // "object"  (1)

typeof null; // "object"  (2)

typeof alert; // "function"  (3)
```

## 交互：alert、prompt 和 confirm

### alert

显示一条信息，并等待用户按下 OK。
{% asset_img 1.png %}

### prompt

`prompt`函数接收两个参数：
`result = prompt(title,[default]);`

`title`：显示给用户的文本
`default`：可选的第二个参数，指定 input 框的初始值
举个例子：

```javascript
let age = prompt("How old are you?", 100);
```

{% asset_img 2.png %}

### confirm

语法：

```javascript
result = confirm(question);
```

`confirm`函数显示一个带有`question`以及确定和取消两个按钮的模态窗口。
点击确定返回`true`，点击取消返回`false`。

{% asset_img 3.png %}

## 类型转换

### 字符串转换

显示调用`String(value)`来将 value 转换为字符串类型。

### 数字型转换

在算术函数和表达式中，会自动进行 number 类型转换。
我们也可以使用`Number(value)`显式地将这个`value`转换为 number 类型。
当然如果字符串不是一个有效数字，转换的结果会是`NaN`。
number 类型转换规则：
{% asset_img 4.png %}

### 布尔类型转换

直观上为“空”的值（如 0、空字符串、`null`、`undefined`和`NaN`）将变为`false`。
其他值变为`true`。

## 基础运算符，数学

### 数学

- 加法：+
- 减法：-
- 乘法：\*
- 除法：/
- 取余：%
- 求幂：\*\*

### 用二元运算符 + 连接字符串

`+`可以合并各个字符串。
注意：只要任意一个运算元是字符串，那么另一个运算元也将被转化为字符串，类似`1+'2'`的情况，最后结果为`'12'`。
当然，如果是`2+2+'1'`结果为`'41'`而不是`'221'`，因为在转换为字符串之前先执行加法运算。
`+`是唯一一个以这种方式支持字符串的运算符。其他算术运算符只对数字起作用，并且总是将其运算元转换为数字。

### 数字转化，一元运算符 +

加号`+`后面跟着一个非数字类型，则会把它转化为数字。

```javascript
// 对数字无效
let x = 1;
alert(+x); // 1

let y = -2;
alert(+y); // -2

// 转化非数字
alert(+true); // 1
alert(+""); // 0
```

效果类似`Number(...)`，但更简短。

### 运算符优先级

[优先级表](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)
建议收藏，随时查阅。

### 赋值运算符

语句`x = value`将值`value`写入`x`**然后返回 x**。

### 原地修改

`+=`、`-=`之类的在 JavaScript 中依然有效。

### 自增/自减

`++`和`--`在 JavaScript 中的作用与在其他语言中的作用类似，故不再赘述。
同样要注意自增/自减符号放在变量前面和后面时的区别。

### 位运算符

- 按位与 &
- 按位或 |
- 按位异或 ^
- 按位非 ~
- 左移 <<
- 右移 >>
- 无符号右移 >>>

### 逗号运算符

逗号运算符只有**最后的语句**的结果会被返回。

## 值的比较

大致与其他语言相同。
不同类型在比较时会进行类型转换，主要是字符串转为数字以及其他类型转换为布尔类型两种情况需要注意。

注意 JavaScript 存在一种**严格相等**的情况，由`===`表示。
由于 JavaScript 中`==`符号无法区分 0 和`false`，所以需要`===`这样的无视类型转换直接比较的运算符。

> 注意`null = undefined`但是`null === undefined`不成立。它们在`==`比较时没有进行类型转换。当使用>= <= > <时，null 被转换为 0，undefined 转换为 NaN。

## 条件分支：if 和'?'

if 语句与其他语言相似，不多赘述。
主要是'?'的使用不大一样。
其中一个语法与其他语言相似，即：

```javascript
let result = condition ? value1 : value2;
```

当然，可以使用多个'?'运算符，来模拟 if...else...的效果：

```javascript
if (age < 3) {
  message = "Hi, baby!";
} else if (age < 18) {
  message = "Hello!";
} else if (age < 100) {
  message = "Greetings!";
} else {
  message = "What an unusual age!";
}
```

## 逻辑运算符

在 JavaScript 中有一种神奇的用法。
因为 JavaScript 中`||`和`&&`有以下特性：

- `||`左侧为假时才会依次计算右侧的值，若左侧为真则直接返回当前值。若全为假则返回最后一个值。
- `&&`左侧为真时才会依次计算右侧的值，若左侧为假则直接返回当前值。若全为真则返回最后一个值。

所以：

```javascript
alert(1 || 0); // 1（1 是真值）

alert(null || 1); // 1（1 是第一个真值）
alert(null || 0 || 1); // 1（第一个真值）

alert(undefined || null || 0); // 0（都是假值，返回最后一个值）

// 如果第一个操作数是真值，
// 与运算返回第二个操作数：
alert(1 && 0); // 0
alert(1 && 5); // 5

// 如果第一个操作数是假值，
// 与运算将直接返回它。第二个操作数会被忽略
alert(null && 5); // null
alert(0 && "no matter what"); // 0
```

## 空值合并运算符'??'

`a ?? b`的结果是：

- 如果`a`是已定义的，则结果为`a`。
- 如果`a`不是已定义的，则结果为`b`。

换句话说，如果第一个参数不是`null/undefined`，则??返回第一个参数，否则返回第二个参数。

> `??`禁止与`&&`和`||`一起使用。

## 循环：while 和 for

### while 循环

```javascript
while (condition) {
  //代码
  //所谓的循环体
}
```

### do...while 循环

```javascript
do {
  // 循环体
} while (condition);
```

### for 循环

```javascript
for (begin; condition; step) {
  // ……循环体……
}
```

## switch 语句

```javascript
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}
```

**类型很关键**，在 JavaScript 中必须时刻注意类型的问题。

## 函数

### 函数声明

函数声明大概就像这个样子：

```javascript
function name(parameter1, parameter2, ... parameterN) {
  ...body...
}
```

关于局部变量和外部变量的问题：

- 函数对外部变量拥有**全部**的访问权。函数也可以修改外部变量。
- 只有在没有局部变量的情况下才会使用外部变量。如果函数内部声明了同名变量，那么函数会**遮蔽**外部变量。

### 默认值

可以使用`=`为函数声明中的参数指定所谓的“默认”值：

```javascript
function showMessage(from, text = "no text given") {
  alert(from + ": " + text);
}

showMessage("Ann"); // Ann: no text given
```

### 返回值

使用`return`关键字。
`return`可以在函数的任意位置。当执行到达时，函数停止，并将值返回给调用代码。
只使用`return`但没有返回值也是可行的。但这会导致函数立即退出。

> 空值的`return`或没有`return`的函数返回值为`undefined`。

## 函数表达式

另一种创建函数的语法称为**函数表达式**。
例如：

```javascript
let sayHi = function () {
  alert("Hello");
};
```

### 函数是一个值

在 JavaScript 中，函数是一个值，所以我们可以把它当成值对待。

```javascript
function sayHi() {
  // (1) 创建
  alert("Hello");
}

let func = sayHi; // (2) 复制

func(); // Hello     // (3) 运行复制的值（正常运行）！
sayHi(); // Hello    //     这里也能运行（为什么不行呢）
```

### 回调函数

```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes();
  else no();
}

function showOk() {
  alert("You agreed.");
}

function showCancel() {
  alert("You canceled the execution.");
}

// 用法：函数 showOk 和 showCancel 被作为参数传入到 ask
ask("Do you agree?", showOk, showCancel);
```

### 函数声明 vs 函数表达式

它们之间除了看上去的明显差别之外，还有一些细微差别。

- **函数表达式是在代码执行到达时被创建，并且仅从那一刻起可用**
- **在函数声明被定义之前，它就可以被调用**

> 在严格模式下，当一个函数声明在一个代码块内时，它在该代码块内的任何位置都是可见的。但在代码块外不可见。

## 箭头函数，基础知识

```javascript
let func = (arg1, arg2, ..., argN) => expression;
```

`(a,b)=>a+b`表示一个函数接受两个名为`a`和`b`的参数。在执行时，它将对表达式`a+b`求值，并返回计算结果。

### 多行的箭头函数

如果需要一些更复杂的东西，可以将内容用花括号括起来，然后使用一个`return`语句返回想要返回的值。

```javascript
let sum = (a, b) => {
  // 花括号表示开始一个多行函数
  let result = a + b;
  return result; // 如果我们使用了花括号，那么我们需要一个显式的 “return”
};

alert(sum(1, 2)); // 3
```
