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


### 糟糕的注释
新手倾向于使用注释来解释“代码中发生了什么”。
在良好的代码中，这种“解释性”评论的数量应该是最小的。严肃的说，就算没有它们，代码也应该很容易理解。
关于这一点有一个很棒的原则：“如果代码不够清晰以至于需要一个注释，那么或许它应该被重写。”


一个好的开发者的标志之一就是他的注释：它们的存在甚至它们的缺席。
好的注释可以使我们更好的维护代码，并且在很长时间之后依然可以更高效地回到代码中和使用其功能。

### 注释这些内容

整体架构，高层次的观点。
函数的用法。
重要的解决方案，特别是在不是很明显时。

### 避免注释

阐述“代码如何工作”或“它做了什么”。
只有在没有这些就不可能使代码变得如此简单和自我描述的情况下才可以使用它们。


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

根据规范，对象的属性键只能是 String 类型或者 Symbol 类型。不是 Number，也不是 Boolean，只有 String 或 Symbol 这两种类型。

在 JavaScript 中，this 是『自由』的，它的值是在调用时进行求值的，它的值并不取决于方法声明的位置，而是（取决）于在『点之前』的是什么对象。


有一个可以上下移动的 ladder 对象：
```js
let ladder = {
  step: 0,
  up() {
    this.step++;
  },
  down() {
    this.step--;
  },
  showStep: function() { // shows the current step
    alert( this.step );
  }
};
```
现在如果我们要依次执行几次调用，可以这样做：
```js
ladder.up();
ladder.up();
ladder.down();
ladder.showStep(); // 1
```
修改 up 和 down 的代码让调用可以链接，就像这样：

```ladder.up().up().down().showStep(); // 1```
此种方法在 JavaScript 库中被广泛使用。

打开带有测试的沙箱。

解决方案
解决方案就是在每次调用后返回这个对象本身。

```js
let ladder = {
  step: 0,
  up() {
    this.step++;
    return this;
  },
  down() {
    this.step--;
    return this;
  },
  showStep() {
    alert( this.step );
    return this;
  }
}

ladder.up().up().down().up().down().showStep(); // 1
```
我们也可以每行一个调用。对于长链接它更具可读性：
```js
ladder
  .up()
  .up()
  .down()
  .up()
  .down()
  .showStep(); // 1
