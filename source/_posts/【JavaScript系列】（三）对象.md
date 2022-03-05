---
title: 【JavaScript系列】（三）对象
date: 2022-03-05 14:38:34
tags:
  - JavaScript
  - 编程语言
  - 前端
categories: 计算机
---

# 对象（基础知识）

## 对象

对象用于存储键值对和更复杂的实体。
我们可以通过使用带有可选**属性列表**的花括号`{...}`来创建对象。一个属性就是一个键值对("key:value")，其中键（key）是一个字符串（也叫做属性名），值（value）可以是任何值。
我们可以用下面两种语法中的任意一种来创建一个空的对象：

```javascript
let user = new Object(); //构造函数的语法
let user = {}; //字面量的语法
```

### 文本和属性

我们在创建对象的时候，可以立即将一些属性以键值对的形式放到`{...}`中。

```javascript
let user = {
  name: "John",
  age: 30,
};
```

可以使用点符号访问属性值：

```javascript
alert(user.name);
alert(user.age);
```

添加一个属性直接使用赋值运算符：

```javascript
user.isAdmin = true; //向user中添加了一个isAdmin: true的键值对
```

可以使用`delete`操作符移除属性：

```javascript
delete user.age;
```

我们也可以用多字词语来作为属性名，但必须加上引号：

```javascript
let user = {
  name: "John",
  age: 30,
  "likes birds": true,
};
```

列表中的最后一个属性最好以逗号结尾：

```javascript
let user = {
  name: "John",
  age: 30,
};
```

这个叫做尾随或悬挂逗号，便于添加、删除和移动属性。

### 方括号

对于多词属性，点操作就不能用了：

```javascript
user.likes birds = true; //错误
```

使用方括号，可以用于任何字符串：

```javascript
let user = {};

// 设置
user["likes birds"] = true;

// 读取
alert(user["likes birds"]); // true

// 删除
delete user["likes birds"];
```

注意方括号中的字符串要放在引号中，单引号或双引号都可以。

还有另一种用法：

```javascript
let key = "likes birds";

// 跟 user["likes birds"] = true; 一样
user[key] = true;
```

注意 key 要放在方括号内，此时的 key 表示的就是"likes birds"。若不加方括号，该语句的意思就变为在 user 对象中获取 key 键的对应值，很明显不正确。

#### 计算属性

当创建一个对象时，我们可以在对象字面量中使用方括号。这叫做**计算属性**。

```javascript
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
  [fruit]: 5, // 属性名是从 fruit 变量中得到的
};

alert(bag.apple); // 5 如果 fruit="apple"
```

`[fruit]`含义是属性名应该从`fruit`变量中获取。
所以，如果一个用户输入`"apple"`，`bag`将成为`{apple: 5}`。

### 属性值简写

一个例子：

```javascript
function makeUser(name, age) {
  return {
    name: name,
    age: age,
    // ……其他的属性
  };
}

let user = makeUser("John", 30);
alert(user.name); // John
```

属性名和变量名一样，这种通过变量生成属性的应用场景很常见，在这有一种特殊的**属性值缩写**方法，是属性名变得更短。
可以用`name`来代替`name: name`：

```javascript
function makeUser(name, age) {
  return {
    name, // 与 name: name 相同
    age, // 与 age: age 相同
    // ...
  };
}
```

### 属性名称限制

对象的属性名可以是某个保留字。
属性名可以是任何字符串或者 symbol。其他类型会被自动地转换为字符串。
例如，当数字 0 被用作对象的属性的键时，会被转换为字符串`"0"`：

```javascript
let obj = {
  0: "test", // 等同于 "0": "test"
};

// 都会输出相同的属性（数字 0 被转为字符串 "0"）
alert(obj["0"]); // test
alert(obj[0]); // test (相同的属性)
```

### 属性存在性测试，"in"操作符

JavaScript 的对象有一个需要注意的特性：能够被访问任何属性。即使属性不存在也不会报错。

```javascript
let user = {};

alert(user.noSuchProperty === undefined); // true 意思是没有这个属性
```

有一个特别的，检查属性是否存在的操作符`in`。
语法是：

```javascript
"key" in object;
```

`in`的左边必须是**属性名**。通常是一个带引号的字符串。若省去引号，就意味着左边是一个变量，它应该包含要判断的实际属性名。

### "for...in"循环

为了遍历一个对象的所有键（key），可以使用一个特殊形式的循环：`for...in`。
语法：

```javascript
for (key in object) {
  //code
}
```

#### 像对象一样排序

对象中有“特殊的顺序”：整数属性会被进行排序，其他属性则按照创建的顺序显示。

> 这里的整数属性指的是一个可以在不做任何更改的情况下与一个整数进行相互转换的字符串。
> 例如："12"则为整数属性，"+12"、"1.2"等则不是整数属性。

## 对象引用和复制

**赋值了对象的变量存储的不是对象本身，而是该对象“在内存中的地址”——换句话说就是对该对象的“引用”。**

**当一个对象变量被复制——引用被复制，而该对象自身并没有被复制。**

### 通过引用来比较

仅当两个对象为同一个对象的时候，两者才相等。

```javascript
let a = {};
let b = a; // 复制引用

alert(a == b); // true，都引用同一对象
alert(a === b); // true
```

两个独立的对象并不相等，即使可能它们看起来一样。

```javascript
let a = {};
let b = {}; // 两个独立的对象

alert(a == b); // false
```

### 克隆与合并，Object.assign

如果想要复制一个对象，而不是引用同一个对象，那就需要创建一个新对象，并通过遍历现有属性的结构，在原始类型值的层面，将其复制到新对象，以复制已有对象的结构。
例子：

```javascript
let user = {
  name: "John",
  age: 30,
};

let clone = {}; // 新的空对象

// 将 user 中所有的属性拷贝到其中
for (let key in user) {
  clone[key] = user[key];
}

// 现在 clone 是带有相同内容的完全独立的对象
clone.name = "Pete"; // 改变了其中的数据

alert(user.name); // 原来的对象中的 name 属性依然是 John
```

我们也可以使用`Object.assign`方法来达成同样的效果。
语法是：

```javascript
Object.assign(dest,[src1,src2,src3,...])
```

例子：

```javascript
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

// 将 permissions1 和 permissions2 中的所有属性都拷贝到 user 中
Object.assign(user, permissions1, permissions2);

// 现在 user = { name: "John", canView: true, canEdit: true }
```

如果被拷贝的属性的属性名已经存在，那么它会被覆盖。

所以可以用`Object.assign`代替`for...in`循环来进行简单克隆：

```javascript
let user = {
  name: "John",
  age: 30,
};

let clone = Object.assign({}, user);
```

### 深层克隆

如果属性是对象的话，以上方法就不太够用了。
为了解决这个问题，我们应该使用一个拷贝循环来检查`user[key]`的每个值，如果它是一个对象，那么也复制它的结构。
可以采用现有的实现，例如[lodash](https://lodash.com/)库的[\_.cloneDeep(obj)](https://lodash.com/docs#cloneDeep)。

## 垃圾回收

### 可达性

JavaScript 中主要的内存管理概念是**可达性**。

1. 这里列出固有的可达值的基本集合，这些值明显不能被释放。
   比如说：
   - 当前执行的函数，它的局部变量和参数。
   - 当前嵌套调用链上的其他函数、它们的局部变量和参数。
   - 全局变量。
   - （还有一些内部的）
2. 如果一个值可以通过引用或引用链从根（即 1 中的值）访问任何其他值，则认为该值是可达的。

在 JavaScript 引擎中有一个被称作垃圾回收器的东西在后台执行。它监控着所有对象的状态，并删除掉那些已经不可达的。

## 对象方法，“this”

### 方法示例

例子：

```javascript
let user = {
  name: "John",
  age: 30,
};

user.sayHi = function () {
  alert("Hello!");
};

user.sayHi(); // Hello!
```

这里我们使用函数表达式创建了一个函数，并将其指定给对象的`user.sayHi`属性。
作为对象属性的函数被称为**方法**。
当然，我们也可以使用预先声明的函数作为方法，就像这样：

```javascript
let user = {
  // ...
};

// 首先，声明函数
function sayHi() {
  alert("Hello!");
}

// 然后将其作为一个方法添加
user.sayHi = sayHi;

user.sayHi(); // Hello!
```

#### 方法简写

```javascript
// 这些对象作用一样

user = {
  sayHi: function () {
    alert("Hello");
  },
};

// 方法简写看起来更好，对吧？
let user = {
  sayHi() {
    // 与 "sayHi: function(){...}" 一样
    alert("Hello");
  },
};
```

### 方法中的“this”

**为了访问该对象，方法中可以使用`this`关键字。**
举个例子：

```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // "this" 指的是“当前的对象”
    alert(this.name);
  },
};

user.sayHi(); // John
```

### “this”不受限制

在 JavaScript 中，`this`关键字与其他大多数编程语言中的不同。JavaScript 中的`this`可以用于任何函数，即使它不是对象的方法。
`this`的值是在代码运行时计算出来的，它取决于代码的上下文。
例如：

```javascript
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert(this.name);
}

// 在两个对象中使用相同的函数
user.f = sayHi;
admin.f = sayHi;

// 这两个调用有不同的 this 值
// 函数内部的 "this" 是“点符号前面”的那个对象
user.f(); // John（this == user）
admin.f(); // Admin（this == admin）

admin["f"](); // Admin（使用点符号或方括号语法来访问这个方法，都没有关系。）
```

### 箭头函数没有自己的“this”

箭头函数有些特别：它们没有自己的`this`。如果我们在这样的函数中引用`this`，`this`值取决于外部“正常的”函数。
举个例子：

```javascript
let user = {
  firstName: "Ilya",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  },
};

user.sayHi(); // Ilya
```

## 构造器和操作符“new”

### 构造函数

构造函数在技术上是常规函数。不过有两个约定：

1. 它们的命名以大写字母开头。
2. 它们只能由`new`操作符来执行。

例如：

```javascript
let user = new User("Jack");
```

### 构造器的 return

如果`return`返回的是一个对象，则返回这个对象，而不是`this`。
如果`return`返回的是一个原始类型，则忽略。

### 构造器中的方法

例子：

```javascript
function User(name) {
  this.name = name;

  this.sayHi = function () {
    alert("My name is: " + this.name);
  };
}

let john = new User("John");

john.sayHi(); // My name is: John

/*
john = {
   name: "John",
   sayHi: function() { ... }
}
*/
```

## 可选链 “?.”

如果可选链`?.`前面的值为`undefined`或者`null`，它会停止运行并返回`undefined`。
**为了简明起见，在本文接下来的内容中，我们会说如果一个属性既不是`null`也不是`undefined`，那么它就“存在”。**
换句话说，例如`value?.prop`：

- 如果`value`存在，则结果与`value.prop`相同。
- 如果不存在，则返回`undefined`。

### 短路效应

如果`?.`左边部分不存在，就会立即停止运算。（短路效应）
所以，如果后面有任何函数调用或者副作用，它们均不会执行。
例如：

```javascript
let user = null;
let x = 0;

user?.sayHi(x++); // 没有 "sayHi"，因此代码执行没有触达 x++

alert(x); // 0，值没有增加
```

### 其他变体：?.(),?.[]

`?.()`调用一个可能不存在的函数。
`?.[]`也类似。
此外，我们还可以将`?.`跟`delete`一起使用。

## Symbol 类型

### Symbol

“Symbol”值表示唯一的标识符。
可以使用`Symbol()`来创建这种类型的值。

```javascript
let id = Symbol();
```

创建时，我们可以给 Symbol 一个描述。

```javascript
let id = Symbol("id");
```

Symbol 保证是唯一的，即使它们的描述相同，它们的值也不同。

### “隐藏”属性

Symbol 允许我们创建对象的“隐藏属性”，代码的任何其他部分都不能意外访问或重写这些属性。

#### 对象字面量中的 Symbol

如果我们要在对象字面量`{...}`中使用 Symbol，则需要使用方括号把它括起来。

```javascript
let id = Symbol("id");

let user = {
  name: "John",
  [id]: 123, // 而不是 "id"：123
};
```

#### Symbol 在 for...in 中会被跳过

Symbol 属性不参与`for...in`循环。

相反，Object.assign 会同时复制字符串和 Symbol 属性。

### 全局 Symbol

有时我们想要名字相同的 Symbol 具有相同的实体。为了实现这一点，这里有一个**全局 Symbol 注册表**。我们可以在其中创建 Symbol 并在稍后访问它们，它可以确保每次访问相同的名字的 Symbol 时，返回的都是相同的 Symbol。
要从注册表中读取（不存在则创建）Symbol，请使用`Symbol.for(key)`。
例如：

```javascript
// 从全局注册表中读取
let id = Symbol.for("id"); // 如果该 Symbol 不存在，则创建它

// 再次读取（可能是在代码中的另一个位置）
let idAgain = Symbol.for("id");

// 相同的 Symbol
alert(id === idAgain); // true
```

#### Symbol.keyFor

`Smybol.keyFor(sym)`，它的作业完全反过来：通过全局 Symbol 返回一个名字。
例如：

```javascript
// 通过 name 获取 Symbol
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// 通过 Symbol 获取 name
alert(Symbol.keyFor(sym)); // name
alert(Symbol.keyFor(sym2)); // id
```

## 对象——原始值转换

### 转换规则

1. 所有的对象在布尔上下文中均为`true`。所以对于对象，不存在 to-boolean 转换，只有字符串和数值转换。
2. 数值转换发生在对象相减或应用数学函数时。
3. 至于字符串转换——通常发生在我们像`alert(obj)`这样输出一个对象和类似的上下文中。

### Symbol.toPrimitive

有一个名为`Symbol.toPrimitive`的内建 symbol，它被用来给转换方法命名：

```javascript
obj[Symbol.toPrimitive] = function (hint) {
  // 这里是将此对象转换为原始值的代码
  // 它必须返回一个原始值
  // hint = "string"、"number" 或 "default" 中的一个
};
```

### toString/valueOf

#### 转换可以返回任何原始类型

唯一强制性的事情是：这些方法必须返回一个原始值，而不是对象。

### 进一步的转换

如果我们将对象作为参数传递，则会出现两个阶段：

1. 对象被转换为原始值。
2. 如果生成的原始值的类型不正确，则继续进行转换。

例如：

```javascript
let obj = {
  // toString 在没有其他方法的情况下处理所有转换
  toString() {
    return "2";
  },
};

alert(obj * 2); // 4，对象被转换为原始值字符串 "2"，之后它被乘法转换为数字 2。
```
