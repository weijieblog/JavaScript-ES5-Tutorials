## 变量与内存
程序在运行的时候，它的指令和变量是存放在计算机内存里的。我们可以把计算机内存想象成一本巨大的笔记本，因而当我们通过 `var` 声明了一个变量，就相当于告诉 JavaScript 让它想办法从这本笔记本中找到几页可以写作的地方，并且在那个地方放置一个书签（变量名），以便我们在需要的时候可以迅速的通过书签找到那个地方，而 JavaScript 的垃圾回收机制会自动的在我们不需要这个书签的时候默默的把那个地方还原为可以写作的状态，防止笔记本被写满。

```javascript
  var a; // JavaScript 在内存中找到了几页空白，并给这里放置名字为 a 的书签
  a = 123456; // 往这几页空白写入了数字 123456
  console.log(a); // 通过 a 这个书签，我们能够快速访问到内存中写了 123456 的这个位置，并得到了其中的值
```

<br>
如果声明了名字相同的变量， JavaScript 就会再次利用这个变量名标记的内存位置。

```javascript
  var a; // JavaScript 在内存中找到了几页空白，并给这里放置名字为 a 的书签
  a = 123456; // 往这几页空白写入了数字 123456
  console.log(a); // 通过 a 这个书签，我们能够快速访问到内存中写了 123456 的这个位置
  
  var a; // 再次声明 a
  console.log(a); // 还是会访问到记载了 123456 这个数字的位置
```
## 逗号操作符
待补充...

## 语句和表达式
**表达式** 是一组可以计算出一个数值的有效的代码的集合，[查看](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#表达式(Expressions))。

## 赋值操作符
在 JavaScript 中可以使用 `=` 操作符对变量进行赋值。在 JavaScript 中 `=`（赋值操作符）的含义和数学中的 $$ = $$ （等于号）是不同的。赋值操作符 `=` 的作用是将其右边的数据赋值给左边，即将 `=` 操作符右边的数据，写入左边变量名所标记的那几页内存中，例如：

```javascript
  var a, b, c;
  
  a = 3; // 3 在右边， = 把右边的 3 给左边的 a ，所以这时候 a 的值为 3
  b = 5; // 5 在右边， = 把右边的 5 给左边的 b ，所以这时候 b 的值为 5
  c = a = b; // 先把最右边 b 的值赋给 a，这个时候 a 和 b 的值都为 5，再把 a 的值赋给 c，此时 c 也为 5
  
  console.log(a, b ,c); // 现在 a b c 都为 5
```

<br>
`=` 操作符也可以在声明变量的时候使用，例如：

```javascript
var a = 3,
    b = 5,
    c = a = b;
    
    console.log(a, b ,c); // 现在 a b c 都为 5
```

<br>
`=` 操作符的最右边还可以是表达式，如果最右边是表达式，则先计算表达式的结果，再将结果逐个往左赋值。

```javascript
  var a, b, c;
  a = 1;
  b = 2;
  c = 3;
  
  a = a + b + c; // 这时先计算 a + b + c，也就是 1 + 2 + 3 再把结果赋值给 a
  console.log(a); // 执行完上句代码后 a 的结果为 6
  
  a = a + a; // 这时先计算 a + a，也就是 6 + 6， 再将结果赋值给 a
  console.log(a); // 现在 a 的值是 12
  
  // 这时先计算 a + b + c， 也就是 12 + 2 + 3
  // 然后将结果赋值给 c ，再将 c 的值赋值给 b ，再将 b 的值赋值给 a
  a = b = c = a + b + c; 
  console.log(a, b, c); // 现在 a b c 都为 17
```

## 变量的命名规则
JavaScript 规定标识符只能由**下划线（ _ ），美元符号（ $ ），数字，以及字符（字母或文字）组成，并且不能以数字开头**。而变量名就是标识符的一种，因而必须按照标识符的要求命名，例如：

```javascript
  var _name; // 对的
  var 1name; // 错的，以数字开头
  var na1me; // 对的
  var name1; // 对的
  var $; // 对的
  var _name_; // 对的
  var 唐宋元明清; // 对的，但不推荐使用英文之外的语言给变量起名字
  var お願いだから; // 对的，但不推荐使用英文之外的语言给变量起名字
  var #$%^&*; // 错的
```
<br>
JavaScript 中属于语言语法本身的单词，例如 `var` `function` 等，这类单词叫做**关键字**。还有一些留给语言以后用做关键字的单词，叫做**保留字**，它们都不能用做变量名。

```javascript
   var var; // 错的
   var function; // 错的
   var class; // 错的
   var return; // 错的
```

<br>
目前关键字和保留字一共几十个，随着对 JavaScript 的不断深入，自然而然就知道哪些可以用作变量哪些不可以，如果不小心误用， JavaScript 会报错并提示我们修改变量名，因而不用死记硬背。当然如果有时间自行查阅相关文档了解一下也不是什么坏事。

## 自增操作符与自减操作符
待补充...

## 加，减，乘，除后赋值操作符
待补充...

## 变量练习

1. 我们运行如下代码的时候， JavaScript 在背后默默的为我们做了什么？

 ```javascript
  var username;
 ```
2. 下列代码改了哪里的内存？对内存做了什么改动？
 
 ```javascript
   id = 1234567890123;
 ```
3. 阅读下列代码并回答问题。

 ```javascript
   var a;
   a = 20;
   
   var b, c;
   c = 1 + 2 + 3;
   b = 4;
   var d = c + b;
   
   var e, f, g;
   e = f = g = a - c; // #1
 ```
   a. 代码运行完后各个变量的值是什么？
   b. #1 处赋值的先后顺序是什么？
4. 小明修改了小红编辑过的 JavaScript 文件，阅读下面代码并回答问题。
 
 ```javascript
   /* 小红之前的代码 */
   var x, y, z, u;
   y = 5;
   x = 3;
   z = y % x;
   
   /* 小明新加入的代码 */
   var x, dydx;
   x = 0;
   dydx = 2 * x + 5;
   
   /* 小红之前的代码 */
   y = 19;
   u = (y + z) / x;
 ```
 a. 然后，小红的代码出了 bug 为什么？
 b. 应该如何修改代码，修复小红的 bug。
 
5. 回答下列问题。
 a. ++a 和 a++ 的区别是什么?
 b. --a 和 a-- 的区别是是什么？
 
6. 阅读下列代码， 当代码运行完后 #1～#8 分别输出什么。

 ``` javascript
   var a = 5;
   a += a;
   console.log(a);   // #1
   console.log(a++); // #2
   console.log(++a); // #3
   
   var b = 4;
   b -= 1;
   console.log(b);   // #4
   console.log(--b); // #5
   console.log(b--); // #6
   
   var c = 3;
   c *= 2;
   console.log(c);   // #7
   
   c /= 2;
   console.log(c);   // #8
 ```
7. 用 JavaScript 描述下列数学式子，其中的未知数用变量替代。其中形如 $$ \dfrac{\mathrm{d}y}{\mathrm{d}x} $$ 的用形如 `dydx` 的变量代替。
 * a. $$ \dfrac{1}{2} \times y \times \dfrac{\mathrm{d}x}{\mathrm{d}t} + \dfrac{1}{2} \times x \times \dfrac{\mathrm{d}y}{\mathrm{d}t} $$
 * b. $$ \dfrac{x \times -1 + 12 \times y}{2} \times \dfrac {z} {13} $$
 * c. $$ \dfrac{13 \times 5 }{ \dfrac{\mathrm{d}y}{\mathrm{d}t} } \times 4 + \dfrac{13}{2} \times 2 $$
