变量命名是编程过程中最重要和最复杂的技能之一。快速地浏览变量的命名就知道代码是一个初学者还是有经验的开发者书写的。

```js
let n = 2;

n *= 3 + 5;

alert( n ); // 16 （右侧计算首先进行，和 n *= 8 相同）

*=和赋值=优先级相同

```

```js
以下代码中变量 a、b、c、d 的最终值分别是多少？

let a = 1, b = 1;

let c = ++a; // ?
let d = b++; // ?

```

### 与用户交互的 3 个浏览器指定的函数：

alert
显示信息。
prompt
显示信息要求用户输入文本。点击确定返回文本，或者点击取消或按下 Esc 键，对于所有浏览器来说，其返回值都是。
confirm
显示信息等待用户点击确定或取消。点击确定返回 true，点击取消或 Esc 键返回 false。


### 多个 ‘?’
使用一系列问号 ? 运算符可以返回一个取决于多个条件的值。

如下所示：

```js
let age = prompt('age?', 18);

let message = (age < 3) ? 'Hi, baby!' :
  (age < 18) ? 'Hello!' :
  (age < 100) ? 'Greetings!' :
  'What an unusual age!';

alert( message );

```


我们的眼睛垂直扫描代码。跨越多行的结构比长的水平代码更容易理解。


Never add a newline between return and the value.


函数是行为。所以它们的名字通常是动词。它应该简短且尽可能准确地描述函数的作用。这样读代码的人就能得到正确的线索。

一种普遍的做法是用动词前缀来开始一个函数，这个前缀模糊地描述了这个动作。团队内部必须就前缀的含义达成一致。


### Why there’s a semicolon at the end?
这里可能有个疑问，为什么函数表达式结尾有一个 ;，而函数声明没有：
```js
function sayHi() {
  // ...
}

let sayHi = function() {
  // ...
};
```
答案很简单：

在代码块的结尾是不需要 ;，像 if { ... }，for { }，function f { } 等语法结构后面都不用加。
函数表达式通常这样声明： let sayHi = ...;，作为一个变量。 而不是代码块。不管什么值，建议在语句结尾处建议使用分号 ;。所以这里的分号与函数表达式本身没有任何关系，它只是终止了语句。


A function is a value representing an “action”
字符串或数字等常规值视为 data。

函数可以视为一个 action。

我们可以在变量之间传递他们，并在需要时运行。



糟糕的注释
新手倾向于使用注释来解释“代码中发生了什么”。
### Ordered like an object
Are objects ordered? In other words, if we loop over an object, do we get all properties in the same order they were added? Can we rely on this?

The short answer is: “ordered in a special fashion”: integer properties are sorted, others appear in creation order. The details follow.

As an example, let’s consider an object with the phone codes:
```js
let codes = {
  "49": "Germany",
  "41": "Switzerland",
  "44": "Great Britain",
  // ..,
  "1": "USA"
};

for(let code in codes) {
  alert(code); // 1, 41, 44, 49
}
```