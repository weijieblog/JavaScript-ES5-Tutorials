## 条件语句

现在正式开始进入程序逻辑的领域了，我们在实际开发中，经常需要表达$$ 如果 p 那么 q $$的逻辑，比如：

1. 如果用户提交的信息符合要求，那么允许该用户注册
2. 如果账户的余额不足，那么提示用户充值
3. 如果该用户是女性，那么给她推送化妆品广告

这是程序逻辑中非常重要的一环，结合之前学习的逻辑运算和本章将要学习的条件语句，我们就能够写出表达力强大的程序，指导计算机按照我们的要求运作， JavaScript 为我们提供了`if`语句和`switch`语句两个类型的条件语句。

## 单一 if 语句和条件

单一的`if`语句是最简单的条件语句，下面的伪代码描述了`if`语句的格式：

```
if (条件) {
  当条件的结果为 true 时执行的代码，为 false 则不执行。
}
```

单一`if`语句会让程序按照如下图所示的流程运行。

```{mermaid}
graph TB
  a((开始))
  b{条件}
  c((结束))
  d[执行代码]
    
  a --> b
  b --为真--> d
  b --为假--> c
  d --> c
```

这里有个很重要的概念，就是「条件」，条件在「条件语句」和往后介绍的「循环语句」中会被大量用到，条件语句中的「条件」就是**表达式**，通常情况下是**逻辑表达式**，此时「条件的结果」就是表达式的返回值，例如我们可以按照如下方式使用单一的`if`语句：

```javascript
var a = 0, 
    b = 0,
    c = 0;
    
var one = 1;

// 如果变量 a 的值小于 1 那么将变量 a b c 的值分别赋值为 1 2 3
if (a < 1) {
  a = 1; // 这里会被执行因为 a < 1 的返回值为 true
  b = 2; // 这里会被执行因为 a < 1 的返回值为 true
  c = 3; // 这里会被执行因为 a < 1 的返回值为 true
}

// 如果变量 a 的值大于 one 那么将变量 a b c 的值分别赋值为 111 222 333
if (a > one) {
  a = 111; // 这里不会被执行因为 a > one 的返回值为 false
  b = 222; // 这里不会被执行因为 a > one 的返回值为 false
  c = 333; // 这里不会被执行因为 a > one 的返回值为 false
}

console.log(a, b, c); // 1 2 3
```
当表达式非常复杂时，我们可以将「条件」分成多行写作，例如：

```javascript
var herName = '小柳',
    age = 28;

// 括号中的表达式来自《布尔类型和逻辑运算》章节，返回值是 true
// 此处的「条件」是表达式
if(!(herName !== '小柳') && 
    age < 30 && age > 25 || 
    herName === '柳柳' && 
    age < 25 && age > 20) {
       
    console.log('这里会被执行');
     
}

```

最简单的表达式就是**变量**或者**常量**，因此「条件」可以是单个**变量**或者**值**即，此时「条件的结果」就是变量持有的值或直接就是值本身，例如：

``` javascript
var a = 0, 
    b = 0,
    c = 0;

// 使用 true 值作为「条件」，下边 {...} 中的代码无论如何都会被执行
if (true) {
  a = 11;
  b = 22;
  c = 33;
}

// 使用 false 值作为「条件」，下边 {...} 中的代码无论如何都不会被执行
if (false) {
  a = 1111;
  b = 2222;
  c = 3333;
}

console.log(a, b, c); // 11 22 33

var condition = true;
console.log(condition); // true

// 使用变量作为「条件」
if (condition) {
  console.log('我会被执行');
}

```

JavaScript 通常情况下要求「条件的结果」是**布尔值**，如果不是布尔值，那么 JavaScript 会在背后默默的将它转变为布尔值，这涉及到**隐式类型转换**的知识，是 JavaScript 中不好的一部分，除非对转化的结果非常有自信，否则不推荐使用，例如：

```javascript
// JavaScript 会将 1 转化为 true 所以下边 {..} 中的代码会被执行
if (1) {
  console.log('我会被执行');
}

// JavaScript 会将 null 转化为 false 所以下边 {..} 中的代码不会被执行
if (null) {
  console.log('我不会被执行');
}

// 赋值表达式，JavaScript 会取 i 作为「条件」，而 i 的值是 0
// 0 会被转换为 false 所以下边 {..} 中的代码不会被执行
if (var i = 0) {
  console.log('我不会被执行');
}
```


尽管是 JavaScript 中不好的一部分，但是还是会有许多对转化结果非常有自信的人，他们经常使用 `if(结果非布尔值的条件){...}`这种格式的`if`语句，为了帮助读者看懂他们的代码，下表总结出了常见的转化结果。

<table>
<thead>
 <tr>
  <td>数据类型</td>
  <td>转化为 true</td>
  <td>转化为 false</td>
 </tr>
</thead>
<tbody>
 <tr>
  <td>数字</td>
  <td>任何非零数字</td>
  <td>0 和 NaN</td>
 </tr>
 <tr>
  <td>字符串</td>
  <td>非空字符串</td>
  <td>空字符串</td>
 </tr>
 <tr>
  <td>数组</td>
  <td>总是</td>
  <td>无</td>
 </tr>
 <tr>
  <td>对象</td>
  <td>总是</td>
  <td>无</td>
 </tr>
 <tr>
  <td>undefined</td>
  <td>无</td>
  <td>总是</td>
 </tr>
 <tr>
  <td>null</td>
  <td>无</td>
  <td>总是</td>
 </tr>
</tbody>
</table>

实际上，逻辑运算也可以使用非布尔值。当我们在做逻辑运算的时候使用了非布尔值时，JavaScript 也会按上表的关系将非布尔值转化为布尔值，再进行逻辑运算，除非对结果非常有把握，否则不推荐这么使用，例如：

```javascript
var a = 0 && true;
// 首先 JavaScript 将 0 转化为了 false
// false && true 的结果是 false
console.log(a); // false

var b = !0 && true;
// 首先 JavaScript 将 0 转化为了 false
// !false && true 的结果是 true
console.log(b); // true

// 意外事件
var c = false || '搞事情啊！';
// WTF 居然不是布尔值！？
console.log(c); // '搞事情啊！'

// 意外事件的修复
var d = false || !!'搞事情啊！';
// 首先 JavaScript 将 '搞事情啊！' 转化为了 true
// 然后将 false || !!true，中的 !!true 转化为 true
// false || true 的结果为 true
console.log(d); // true
```
> 上面代码中的意外事件是因为 JavaScript 把`var c = false || '搞事情啊！'`当作了**条件赋值语句**，该语句的用法如下代码描述：

> ```javascript
> var x = y || z;
> ```
> 上边**条件赋值语句**的写法如下流程图描述

```{mermaid}
graph TB
a((开始))
b{y}
c((结束))
d[x=y]
e[x=z]
 
a --> b
b --为真--> d
b --为假--> e
d --> c
e --> c
```

> 出现这种情况也是一种提醒，提醒我们如果不是对转换的结果非常有把握，不推荐在逻辑运算中混合使用布尔值和非布尔值。


## 代码块
在 JavaScript 中，使用`{}`包裹的一系列代码叫做**代码块**，例如下列代码中就有一个代码块：

```javascript
if (true) { /* 代码块开始-> */
  
  var namelist = ['小红'];
  namelist.push('小绿');
  namelist.push('小蓝');
  

/* <-代码块结束 */ }
```

代码块的内容可以是任意合法的 JavaScript 代码，因此代码块也可以包含代码块，在编写程序的时候，常常使用缩进来使得各个代码块之间的关系更加一目了然，例如：

```javascript
if (true) {
  var namelist = ['小红'];
  namelist.push('小绿');
  namelist.push('小蓝');
  
  if (namelist.length > 0) {
    var poped = namelist.pop();
    
    if (poped === '小蓝') {
      console.log(poped);
    }   
  }
  
  if (namelist.length === 0) {  
    console.log('namelist 为空');
  }
}
```
> 小练习：上面的代码中共四个代码块，你能指出分别是哪四个么。

代码块和对象的声明都是使用`{}`包裹着相关的代码，例如：

```javascript
// 声明一个对象
var user = {
  age: 20,
  gender: 'male'
};

// if 语句后边跟着一个代码块
if (true) {
  var namelist = ['小红'];
  namelist.push('小绿');
  namelist.push('小蓝');
}

```
区分它们的方法非常简单，最常见的方法就是，声明对象的时候使用的是固定的，形如`属性名: 属性值,`这种格式的代码，而代码块是任意代码，例如：

```javascript
// 声明一个对象，写法是固定的 属性名: 属性值
var coconut = {
  name: '椰子',
  color: '棕色'
}


// 代码块，可以包含任意代码
{

  var user = {
    age: 20,
    gender: 'male'
  };
  var namelist = ['小红', '小绿', '小蓝'];
  
  // 这里又有一个代码块
  if (namelist.length === 3) {
    console.log(namelist);
  }
  
}
```
> 代码块通常是伴随着某些语句一同出现如`if`语句，代码块也可以单独出现，如上面代码所示。

当然也会有一些不好一眼就分辨的情况，当出现这种情况时，可以通过`{....}`和操作符的位置进行判断，当`{....}`出现在操作符右边时 JavaScript 把它当作就是对象，左边的就是代码块，例如：

```javascript
!{}; // false，{} 被当作对象处理
!{ var a = 1; }; // 语法错误，因为  JavaScript 将 ! 后的 {} 当作了一个对象

{} + 1; // 1，{} 被当作代码块处理
{ var b = 1 } + 1; // 没有语法错误，因为  JavaScript 将 {} 当作了一个代码块，而代码块可以是任意代码

// 报错，左边的 {} 被当成了代码块，右边的 {} 被当成对象
{} = {};

// 对象最常见的用法，不就是在 = 操作符右边么
var c = {
  name: '123'
};
```

当`{...}`被括号`()`包裹的时候， JavaScript 把它当作一个对象，例如：

```javascript
({ var a = 1; }); // 语法错误，因为  JavaScript 将括号中的 {} 当作了一个对象

({a: '123'}); // 没有语法错误
```

## 复合 if 语句

### `if...else...` 语句

当我们需要表达$$如果 p 那么 q 否则 r$$的逻辑时，需要使用`if...else...`语句，下面伪代码描述了该语句的格式：

```
if (条件) {
  代码块 1：当「条件」的结果为 true 时执行这个代码块的内容
} else {
  代码块 2：当「条件」的结果为 false 时执行这个代码块的内容
}
```
上述代码有如下需要注意的地方：

1. JavaScript 对这个语句中「条件」的处理规则和单一`if`语句中介绍的一样。。
1. 结尾的`else {...}`不是必须的，当`else {...}`被去掉时，就成了单一的`if`语句。

下面的流程图给出了`if...else...`语句的执行过程。

```{mermaid}
graph TB
a((开始))
b{条件}
c((结束))
d[代码块 1]
e[代码块 2]
 
a --> b
b --为真--> d
b --为假--> e
d --> c
e --> c
```

下列代码使用了 JavaScript 的`if...else...`语句描述一些常见的逻辑：

```javascript
// 描述用户的对象
var user = {
  age: 20,
  gender: 'male'
};

// 如果用户的年龄大于等于十八岁则显示欢迎词，否则给出警告。
if (user.age >= 18) { // #1
  console.log('欢迎来到电影大世界'); // #2
} else {
  console.log('FBI warning!');
}

// 如果用户为男性则显示欢迎词，否则显示社会主义荣辱观。
if (user.gender === 'male') {  // #3
  console.log('欢迎来到电影大世界');
} else {
  console.log('以服务人民为荣，以背离人民为耻。'); // #4
}
```
运行上面的代码，打印出了两个「欢迎来到电影大世界」。这是因为当程序运行到`#1`处时`user.age >= 18`返回的是`true`，然后程序运行了`#2`所在的代码块的内容，打印了第一个「欢迎来到电影大世界」。然后程序运行到`#3`的时候`user.gender === 'male'`返回了`true`，然后程序运行了`#4`所在的代码块的内容，打印了第二个「欢迎来到电影大世界」。

打印两个相同的欢迎词肯定是有点多余的，为了节约用户的时间，我们利用代码块可以包含代码块的设定，按照如下方式组合俩个`if...else...`语句使得逻辑更精简：

```javascript
// 描述用户的对象
var user = {
  age: 20,
  gender: 'male'
};

// 如果用户的年龄大于等于十八岁则进一步判断性别，否则给出警告。
if (user.age >= 18) {
  // 判断性别，如果用户为男性则显示欢迎词，否则显示社会主义荣辱观。
  if (user.gender === 'male') {
    console.log('欢迎来到电影大世界。');
  } else {
    console.log('以服务人民为荣，以背离人民为耻。');
  }
} else {
  console.log('FBI warning!');
}
```

### `if...else if...else...` 语句
前面介绍的单`if`语句和`if...else...`语句都是简化版本的`if...else if...else...`语句，这才是`if`语句的究极形态，它的伪代码如下：

```
if (条件1) {
  代码块 1：当「条件1」的结果为 true 时执行这个代码块的内容
} else if (条件2) {
  代码块 2：当「条件1」的结果为 false ，但是「条件2」的结果为 true 时执行这个代码块的内容
} else if (条件3) {
  代码块 3：当「条件1」「条件2」的结果都为 false， 但是「条件3」的结果为 true 时执行这个代码块的内容
} else {
  代码块 else：当所有上面所有「条件」的结果都为 false 时执行这个代码块的内容
}
```
上述代码有如下需要注意的地方：

 1. JavaScript 对这个语句中各个「条件」的处理规则和单一`if`语句中介绍的一样。
 2. `else if (条件) {...}`的数量是任意的，当数量为 0 的时候就成了`if...else...`语句。


下面的流程图给出了`if...else if...else...`语句的执行过程。

```{mermaid}
graph TB
S((开始))
T1{条件 1}
T2{条件 2}
T3{条件 3}
T4{条件 N}
E((结束))

B1[代码块 1]
B2[代码块 2]
B3[代码块 3]
B4[代码块 N]
B5[代码块 else]

S --> T1
T1 --为真--> B1
T1 --为假--> T2

T2 --为真--> B2
T2 --为假--> T3

T3 --为真--> B3
T3 --为假--> T4

T4 --为真--> B4
T4 --为假--> B5

B1 --> E
B2 --> E
B3 --> E
B4 --> E
B5 --> E
 
```

从上面的流程图可以看出，无论如何`if...else if...else...`中至多只有一个代码块会运行，如果多个「条件」的结果都为`true`那么，只执行第一个「条件」为`true`的代码块，当全部「条件」的结果都为`false`时，执行`else`后面的代码块，例如：

```javascript
var score = 85,
    result;
    
// 尽管『score >= 0』『score >= 60』 『score < 100』三个条件的结果都是 true
// 但是『score >= 0』是第一个为 true 的，所以 result 等于 1
if (score >= 0) {
  result = 1; // 被执行了
} else if (score >= 60) {
  result = 2;
} else if (score < 100) {
  result = 3;
} else {
  result = 4;
}
console.log(result); // 1


// 尽管『score >= 60』 『score < 100』两个条件的结果都是 true
// 但是『score >= 60』是第一个为 true 的，所以 result 等于 2
if (score === 0) {
  result = 1;
} else if (score >= 60) {
  result = 2; // 被执行了
} else if (score < 100) {
  result = 3;
} else {
  result = 4;
}
console.log(result); // 2

// 所有「条件」的结果都是 false
// 执行 else 之后的代码块，所以 result 等于 4
if (score === 0) {
  result = 1;
} else if (score === 1) {
  result = 2;
} else if (score === 2) {
  result = 3;
} else {
  result = 4;  // 被执行了
}
console.log(result); // 4
```

`if...else if...else...`语句中`else if {...}`的个数可以有无数多个，例如下面各个语句都是合法的：

``` javascript
var score = 85;

// 只有一个 else if {...} 
if (score >= 0 && score < 60) {
  console.log('没及格');  // 没执行，因为 score >= 0 && score < 60 返回 false
} else if (score >= 60 && score <= 100) {
  console.log('及格');  // 执行了， 因为 score >= 60 && score <= 100 返回 true
} else {
  console.log('异常：分数小于 0 或者大于 100'); // 没执行，因为有一个条件的结果是 true
}

// 有多个 else if {...}
if (score >= 0 && score < 20) {
  console.log('分数少于 20'); // 没执行
} else if (score >= 20 && score < 40) {
  console.log('分数在 20 到 40 之间'); // 没执行
} else if (score >= 40 && score < 60) {
  console.log('分数在 40 到 60 之间'); // 没执行
} else if (score >= 60 && score < 80) {
  console.log('分数在 60 到 80 之间'); // 没执行
} else if (score >= 80 && score < 100) {
  console.log('分数在 80 到 100 之间'); // 执行了
} else if (score === 100) {
  console.log('满分'); // 没执行
} else {
  console.log('异常：分数小于 0 或者大于 100'); // 没执行
}
```

当`else if {...}`的个数是零个时，就成了`if...else...`语句，例如：

``` javascript
var score = 85;

// 一个 else if {...} 都没有，就成了 if...else... 语句
if (score >= 0 && score < 100) {
  console.log('正常：分数在正常范围内');
} else {
  console.log('异常：分数小于 0 或者大于 100');
}
```

`if...else if...else...`语句中结尾的`else {...}`不是必须的，例如下面的代码是合法的： 

``` javascript
var score = 85,
    grade;

// 去掉了末尾的 else {...} 
if (score >= 0 && score < 60) {
  grade = '没及格';
} else if (score >= 60 && score <= 100) {
  grade = '及格';
}
console.log(grade); // '及格'

// 去掉了末尾的 else {...} 
if (score >= 0 && score < 60) {
  grade = '没及格';
} else if (score >= 60 && score < 80) {
  grade = '分数在 60 到 80 之间';
} else if (score >= 80 && score < 100) {
  grade = '分数在 80 到 100 之间';
} else if (score === 100) {
  grade = '满分';
}
console.log(grade); // '分数在 80 到 100 之间'
```

当`else if {...}`的个数是零个，并且去掉了末尾的`else {...}`，就成了单`if`语句，例如：

``` javascript
var score = 85,
    grade;

// 去掉了所有 else if {...} 和末尾的 else {...} 就成了单一的 if 语句
if (score >= 0 && score < 100) {
  grade = '分数在 0 到 100 之间';
}

console.log(grade); // '分数在 0 到 100 之间'
```

## 多分枝选择语句 switch

日常编程中，常常需要将某个表达式的值做一系列的比较，根据不同的情况作出不同的行为，例如下面的代码就是根据`title`值的不同，给`greeting`赋不同的值：

``` javascript
var title = '学生',
    greeting;

if (title === '学生') {
  greeting = '祝你学习进步';
} else if (title === '职场人士') {
  greeting = '祝你工作顺利';
} else if (title === '退休人士') {
  greeting = '祝你身体健康';
} else {
  greeting = '你好';
}
console.log(greeting); // '祝你学习进步'
```


为了方便我们处理这种情况， JavaScript 提供了`switch`语句，下边的伪代码描述了`switch`语句的格式：

```
switch (条件) {
  case 结果1:
    当「条件」的结果是「结果1」时执行的分支
    break;
  case 结果2: 
    当「条件」的结果是「结果2」时执行的分支
    break;
  case 结果3: 
    当「条件」的结果是「结果3」时执行的分支
    break;
  default:
    当「条件」没被 case 捕获时执行的分支
}
```

例如，下边`switch`语句和上上方的代码表达的是同样的逻辑：

``` javascript
var title = '学生',
    greeting;

// 根据不同的 title 值作出不同的行为
switch (title) {
  case '学生': 
    greeting = '祝你学习进步'; // 被执行了，因为 title 的值是 '学生'
    break;
  case '职场人士': 
    greeting = '祝你工作顺利'; // 没被执行，因为 title 的值不是 '职场人士'
    break;
  case '退休人士': // 当 title 的值是 '退休人士'
    greeting = '祝你生体健康'; // 没被执行，因为 title 的值不是 '退休人士'
    break;
  default:
    greeting = '你好'; // 没被执行，因为 title 的值不是 '职场人士'
}

console.log(greeting); // '祝你学习进步'
```
> 这里的 `case '学生'` 就相当于 `title === '学生'`。

当「结果」是表达式的时候，比较的就是表达式的返回值，例如：

``` javascript
var age = 28,
    greeting;

switch (true) {
  case age < 18:
    greeting = '你好，同学';
    break;
  case age >= 18 && age < 40:
    greeting = '你好，先生';
    break;
  case age >= 40:
    greeting = '你好，前辈';
    break;
  default:
    greeting = '你好';
}
console.log(greeting); // '你好，先生'
```

同`if`一句的`else if {...}`一样，`switch`语句的`case`可以有任意多个，例如下面代码都是合法的：

``` javascript
var age = 28,
    greeting;
    
// case 有零个
switch (title) {
  default:
    greeting = '你好';
}
console.log(greeting); // '你好'


// case 有三个
switch (title) {
  case '学生':
    greeting = '祝你学习进步';
    break;
  case '职场人士':
    greeting = '祝你工作顺利';
    break;
  case '退休人士':
    greeting = '祝你生体健康';
    break;
  default:
    greeting = '你好';
}
console.log(greeting); // '祝你学习进步'
```

同`if`语句中的`else {...}`一样，`default`在`switch`中不是必须的，例如下面代码是合法的：

``` javascript
var title = '学生',
    greeting;
    
// 省略了 default 的 switch 语句
switch (title) {
  case '学生':
    greeting = '祝你学习进步';
    break; // #1
  case '职场人士':
    greeting = '祝你工作顺利';
    break;
  case '退休人士':
    greeting = '祝你生体健康';
}
// #2
console.log(greeting); // 祝你学习进步
```

`switch`语句中的`break`是让程序提前结束这个`switch`语句，不再运行继续往下执行它。例如，上边代码中`#1`处的的`break`被执行后，程序会直接跳转到代码的`#2`处，期间所有的代码都不再运行。

`switch`语句中，如果程序进入了某个省略了`break`语句的分支，那么程序不仅会执行该分支中的代码，也会执行往后所有分支的代码，直到在再次遇到`break`语句，或者该`switch`语句结束。

``` javascript
var level = 3;

// 从 case 3 处一直到 break 之前所有分支的代码都会被执行
switch(level) {
  case 4:
    console.log('我没被执行');
  case 3:
    console.log('被执行 3'); // 被执行了
  case 2:
    console.log('被执行 2'); // 被执行了
  case 1:
    console.log('被执行 1'); // 被执行了
    break; // 被执行后跳转到 #1 处
  default:
    console.log('没被执行');
}
// #1

// 从 case 3 处一直到语句结束，所有分支的代码都会被执行
switch(level) {
  case 4:
    console.log('我没被执行');
  case 3:
    console.log('被执行 3'); // 被执行了
  case 2:
    console.log('被执行 2'); // 被执行了
  case 1:
    console.log('被执行 1'); // 被执行了
  default:
    console.log('被执行 default'); // 被执行了
}
```

注意`switch`语句后边跟的代码块有着特殊的语法规则，第一层逻辑中只能是`case`，其他任意代码只有在分支里才能书写，例如：

``` javascript
var title = '学生',
    greeting;

switch (title) {
  console.log('语法测试'); // 报错，语法错误，switch 语句代码块中的第一层逻辑中只能是 case
  case '学生':
    greeting = '祝你学习进步';
    break;
  case '职场人士':
  case '退休人士':
    greeting = '祝你工作顺利';
}

switch (title) {
  case '学生':
    if (true) {
      console.log('语法测试'); // 可以正常运行
    }
    greeting = '祝你学习进步';
    break;
  case '职场人士':
  case '退休人士':
    greeting = '祝你工作顺利';
}

```

## 条件语句练习

1. 阅读下面代码，给出变量`a~e`的值。

  ```javascript
  var ten = 10,
      one = 1,
      two = 2,
      three = 3,
      name = 'jackson';

  var a = 0;
  if (name.length >= ten) {
      a = 1;
  } else {
      a = 2;
  }

  var b = 10;
  if (name.slice(3).length >= three) {
      b = 5;
  } else {
      b = 1;
  }

  var c = 0;
  if (c) {
      c = 1;
  }

  var d = 20;
  if (!!!true && d > two) {
      d = 5;
  }

  var e = 50;
  if (name) {
      e = 5;
  } else {
      e = 20;
  }
  ```
2. 阅读下列代码，给出变量`a~f`的值。

  ```javascript
  var userInfo = {
      email: '123456@qwert.com',
      cellphone: '12345678901',
      nicename: '萌小绿',
      age: 5,
      gender: 'female',
      hobbies: ['趴窗台', '晒太阳', '玩毛线球', '吃小鱼干']
  };

  var a = 0;
  if (userInfo.id) {
      a = 1;
  } else {
      a = 2;
  }

  var b = 10;
  if (userInfo.gender === 'female') {
      if (userInfo.hobbies.length > 0) {
        b = 5;
      } else {
        b = 4;
      }
  } else {
      b = 1;
  }

  var c = 0;
  if (userInfo.hobbies.indexOf('晒太阳') !== -1) {
      c = 1;
      if (userInfo.hobbies.length > 1) {
        c = userInfo.hobbies.length;
      } else {
        c = 2;
      }
  } else {
      if (userInfo.age >= 20) {
        c = 3
      }
  }

  var d = 20;
  if (userInfo.nicename = '喵小绿') {
      d = 5;
      if (userInfo.hobbies.indexOf('吃小鱼干') === -1) {
        d = 6;
      } else {
        d = 7;
      }
  } else {
      d = 8;
  }

  var e = 50;
  if (name) {
      e = 5;
  }
  
  var f = 0;
  if (userInfo.hobbies) {
      f = 5;
  }
  ```
3. 下面的代码是合法的，为什么？有多少个代码块，有多少个对象？
 
  ```javascript
  {
      {
        {
          {var cat = {name: 'Yoyo'};}
        }
      }
  }
  ```
4. 一道很经（ken）典（die）的 JavaScript 面试题，为什么`{} + 1`不等于`1 + {}`呢?

4. 阅读下列代码，指出`#1~#12`各个代码块哪里被运行了。
 
  ```javascript
  var commodity = {
      type: '洗发水',
      brand: '飘硬',
      prices: {
        large: 4.99,
        medium: 3.99,
        small: 2.99
      }
  };
  
  if (commodity.prices.large > 5) {
      // #1
  } else if (commodity.prices.large > 4) {
      // #2  
  } else if (commodity.prices.large > 3) {
      // #3
  } else {
      // #4
  }
  
  if (commodity.type === '沐浴露') {
      if (commodity.brand) {
        // #5
      } else if (commodity) {
        // #6
      }
  } else if (commodity.type === '牙膏') {
      if (commodity.prices.small > 3) {
        // #7
      } else if (commodity) {
        // #8
      }
  } else if (commodity.type === '洗衣粉') {
      if (commodity.prices.medium > 4) {
        // #9
      } else if (commodity) {
        // #10
      }
  } else {
      if (commodity.prices.medium > 5) {
        // #11
      } else if (commodity) {
        // #12
      }
  } 
  ```
5. 阅读下列代码，指出`#1~#10`哪处被运行了，哪处没被运行。

    ```javascript
    var book = {
      title: '双城记',
      author: '查尔斯·狄更斯',
      years: 1859,
      prices: {
        paperback: 20,
        hardcover: 35,
        classical: 99
      },
      tabs: ['小说', '英国', '西方文学']
    }
    
    switch(book.title) {
      case 'A Tale of Two Cities':
      case '双城记':
        // #1
      default:
        // #2
    }
    
    switch(true) {
      case book.years >= 1950 && book.years <= 2017:
        // #3
        break;
      case book.years < 1950 && book.years >= 1840:
        // #4
        break;
      case book.years < 1840
        // #5
        break;
      default:
        // #6
    }
    
    switch(book.prices.classical) {
      case '99':
        // #7
      case 99:
        // #8
      case book.prices.classical < 999:
        // #9
      default:
        // #10
    }
    
    ```
7. 当运行下列代码后`#1~#3`处各输出什么。

	``` javascript
	var title = '导盲犬',
	    greeting;
	
	switch (title) {
	  case '学生': 
	    greeting = '祝你学习进步';
	    break;
	  case '职场人士':
	    greeting = '祝你工作顺利';
	    break;
	  case '退休人士':
	    greeting = '祝你生体健康';
	    break;
	  default:
	    greeting = '你好';
	}
	console.log(greeting); // #1
	
	switch (title) {
	  case '学生': 
	    greeting = '祝你学习进步';
	    break;
	  case '职场人士': 
	  case '退休人士': 
	  case '导盲犬':
	    greeting = '祝你工作顺利';
	    break;
	  default:
	    greeting = '你好';
	}
	console.log(greeting); // #2
	
	var test = 'hello';
	switch (title) {
	  case '学生': 
	    greeting = '祝你学习进步';
	    break;
	  case '职场人士': 
	  case '退休人士': 
	  case '导盲犬':
	    greeting = '祝你工作顺利';
	  default:
	    test = '你好个毛';
	}
	console.log(test, greeting); // #3
	```
6. 有如下两个数据，按照要求写出相应代码。

    ```javascript
    var user = {
      name: '花花',
      gender: 'female'
    },
    greeting;
    ```
    
    * a. 使用`if`语句根据用户性别（gender）为`greeting`赋值，性别是`'male'`赋值为`'先生，你好。'`性别是  `'female'`赋值为`'女士，你好'`。
    * b. 使用`switch`语句完成上述要求。
    
9. 用户等级，一个电商网站需要根据用户的年消费额给用户划分 vip 等级，额度和等级的对应方式如下表。

   <table>
    <thead>
     <tr>
      <td>消费额度（spending）</td>
      <td>等级(level)</td>
     </tr>
    </thead>
    <tbody>
     <tr>
      <td>一万以下</td>
      <td>VIP</td>
     </tr>
     <tr>
      <td>一万到三万（含）</td>
      <td>黄金 VIP</td>
     </tr>
     <tr>
      <td>三万以上</td>
      <td>钻石 VIP</td>
     </tr>
    </tbody>
   </table>
   
   * a. 使用`if`语句编写代码，根据不同的`spending`值给`level`赋上相应的值。
   * b. 使用`switch`语句完成上面的需求。
 
10. 编写程序判断变量`num`是奇数还是偶数，如果是奇数给变量`result`赋值为`'odd'`，如果是偶数给变量`result`赋值为`'even'`，提示：判断奇偶可以使用取模运算。

7. 有大小不等的`num1` `num2` `num3`三个数字和一个`result`数组，编写程序让无论`num1` `num2` `num3`取何数字（但彼此不能相等），它们都能按照从小到大的顺序作为数组的成员，例如：
    
    ```
    假设一开始 num1 = 23、num2 = 888、num3 = 2、result = [] 即：
    var num1 = 23, 
        num2 = 888, 
        num3 = 2,
        result = [];
    
    经过「你编写的代码」后...
    
    console.log(result); // [2, 23, 888]，就是 result 成员为 [num3, num1, num2]
    
    注意，无论 num1 、num2 、num3 取何值，经过「你编写的代码」后，它们都能按照从小到大的顺序成为 result 的成员
    
    ```
8. 将上一题的顺序改为从大到小排列。