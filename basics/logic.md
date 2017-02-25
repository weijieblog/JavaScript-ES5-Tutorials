## 命题
先介绍一个数学概念——**命题**。命题是一个陈述句，它的结果或 **真** 或 **假** ，只能二者选其一。

例如下面的陈述句全部都是命题。
1. 1 + 1 = 2
2. 1 > 2
3. 2 > 1
4. 中华人民共和国的首都是北京
5. 人类文明诞生在火星

当一个命题的结果为真，我们就称该命题是**真命题**，当一个命题的结果为假我们就称该命题为**假命题**。
上述的命题中 1 3 4 是真命题， 2 5 是假命题。

下列句子就不是命题。
1. 韦捷是变态吗？
2. x + y = 2
3. 你过来一下。

1 不是命题，因为不是陈述句， 2 3 也不是命题，因为它们没有真假可言。

## 布尔类型数据
布尔类型的数据是由 `true`(真) 或 `false`(假) 两个值组成，二者选其一，表示命题的结果。在 JavaScript 中，我们可以用如下方式使用布尔类型数据或声明布尔类型的变量，例如：

``` javascript
// 直接使用布尔类型数据
false;
true;
  
// 声明布尔类型的变量
var a = true;
var b = false;
```

<br>
在 JavaScript 用**逻辑表达式**来描述命题，它属于表达式的一种，返回的结果是布尔类型的数据，例如下列代码中的`1 > 2`和`1 < 2`：

```javascript
// 比较操作， > 表示大于， < 表示小于，它们都是关系操作符，下文会介绍
var d = 1 > 2;
console.log(d); // 输出 false 表示 1 > 2 为假
var e = 1 < 2;
console.log(e); // 输出 true 表示 1 < 2 为真  
```

## 逻辑操作符
数学有对命题进行**否定**，**合取**，**析取**的操作。同样的 JavaScript 给我们提供了三种**逻辑操作符**来组成逻辑表达式，它们分别是 `!`（逻辑非操作符）， `||`（逻辑或操作符）， `&&`（逻辑与操作符），下面将逐个介绍这三个操作符的用法。

### 逻辑非操作符
编程中的逻辑非，就相当于数学中的否定。对一个命题进行否定，就得到该命题的**否命题**。有如下定理：
> 如果一个命题为真，那么它的否命题为假。如果一个命题为假，那么它的否命题为真。

<br>
例如：
$$ p: 北京是中华人民共和国的首都 $$

的否命题就是，

$$ q: 北京不是中华人民共和国的首都 $$

我们知道 $$p$$ 的结果为真，依据上述定理，那么 $$q$$ 的结果就为假，符合常识。

<br>
再有：

$$ p: 北京不是中华人民共和国的首都 $$

的否命题就是，

$$ q：北京是中华人民共和国的首都 $$

我们知道 $$p$$ 的结果为假，依据上述定理，那么 $$q$$ 的结果就为真，同样符合常识。

JavaScript 以及许多编程语言中用 `!` （逻辑非操作符）表达否定，所以我们有:

``` javascript
var a = true;
var b = false;
  
console.log(!a); // 输出 false
console.log(!b); // 输出 true 
  
var c = !(1 < 2);
console.log(c); // 输出 false
  
var d = !(1 > 2);
console.log(d); // 输出 true
```

<br>
当多个 `!` 连用时：

```javascript
!!!true; // false
```
求值过程如下：

```javascript
// 原式
!!!true;

// 先处理被括号标记的内容 !!【!true】 得到下式
!!false;
  
// 先处理被括号标记的内容 !【!false】 得到下式
!true;
  
// 处理 !true 得结果
false; // 最后结果
```

### 逻辑与操作符
编程中的逻辑与，就相当于数学中的合取，关于合取，有如下定理。
> 令 $$p$$ , $$q$$ 为命题，$$p$$ 和 $$q$$ 的合取即为命题 “$$p$$ 并且 $$q$$”。只有当 $$p$$ 和 $$q$$ 都为真时， “$$p$$ 并且 $$q$$” 才为真，否则 “$$p$$ 并且 $$q$$” 为假。

<br>
例如，昨晚发生了一起抢劫案，警方通过录像判断罪犯身材如姚明般高大，并且是个女人。有如下四个命题:
$$ p：疑犯身高两米以上 $$ （真）
$$ q：疑犯是个女的 $$ （真）
$$ r：疑犯身高不到一米四 $$ （假）
$$ s：疑犯是个男的 $$ （假）

警方抓到了四个嫌犯，特征如下：
1. $$p$$ 合取 $$q$$：身高两米以上，并且是个女的。 （疑犯 A）
2. $$p$$ 合取 $$s$$：身高两米以上，并且是个男的。 （疑犯 B）
3. $$r$$ 合取 $$q$$：身高不到一米四，并且是个女的。（疑犯 C）
4. $$r$$ 合取 $$s$$：身高不到一米四，并且是个男的。（疑犯 D）

观察上述句子就能知道，只有疑犯 A 符合罪犯的特征。疑犯 B 因为“是个男的”被释放，疑犯 C 因为“身高不到一米四”被释放， 疑犯 D 整个都不符合，看了一眼直接释放。于是疑犯 A 被重点审问，而 B C D 洗脱了嫌疑。也就是说，只有 “$$p$$ 合取 $$q$$”为真，因为 $$p$$ 和 $$q$$ 都为真，其余的为假，因为要么其中一个命题为假，要么都为假。

JavaScript 提供 `&&` (逻辑与操作符)来描述合取，例如：

```javascript
// 必须两个子命题都为真时结果才为真，否则为假
console.log(true && true); // true
console.log(false && true); // false
console.log(true && false); // false
console.log(false && false); // false

// 当多个 && 连用时，有一个或多个子命题为假，那么整个命题都为假，否则为真
console.log(false && true && true && true && true && true && true); // false
console.log(false && false && true && true && true && true && true); // false
console.log(true && true && true && true && true && true && true); // true
```

### 逻辑或操作符

编程中的逻辑或就相当于数学中的析取，关于析取，有如下定理：
> 令 $$p$$ , $$q$$ 为命题，$$p$$ 和 $$q$$ 的析取即为命题 “要么 $$p$$ ，要么 $$q$$”。只有当 $$p$$ 和 $$q$$ 都为假时， “要么 $$p$$ ，要么 $$q$$” 才为假，否则 “要么 $$p$$ ，要么 $$q$$” 为真。

<br>
例如，有如下四个命题:
$$ p：北京是中华人民共和国的首都 $$
$$ q：东京是日本国的首都 $$
$$ r：人类生活在火星上 $$
$$ s：人类只有一种性别 $$

我们对上述命题进行如下析取：
1. $$p$$ 析取 $$q$$：要么北京是中华人民共和国的首都，要么东京是日本国的首都。
2. $$p$$ 析取 $$r$$：要么北京是中华人民共和国的首都，要么人类生活在火星上。
3. $$r$$ 析取 $$q$$：要么人类生活在火星上，要么东京是日本国的首都。
4. $$r$$ 析取 $$s$$：要么人类生活在火星上，要么人类只有一种性别。

观察上述句子就能知道，只有第四句话是完全错的。其余的有的前半句对有的后半句对，有的都对。符合常识和也符合上述定理的描述。

JavaScript 提供 `||` (逻辑或操作符)来描述析取，例如：

``` javascript
// 必须两个子命题都为假时结果才为假，否则为真
console.log(true || true); // true
console.log(false || true); // true
console.log(true || false); // true
console.log(false || false); // false

// 当多个 || 连用时，有一个或多个子命题为真，那么整个命题都为真，否则为假
console.log(true || false || false || false || false || false); // true
console.log(true || true || false || false || false || false); // true
console.log(false || false || false || false || false || false); // false
```

### 逻辑操作符优先级

在现实开发中，我们可能会在一个逻辑表达式中同时使用多个逻辑操作符，那么就会涉及到操作符优先级的问题，下面的表格总结了逻辑操作符的优先级，顺序从高到低：

<table>
 <thead>
  <tr>
   <td>操作符类型</td>
   <td>操作符优先级</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>逻辑非</td>
   <td><code>!</code></td>
  </tr>
  <tr>
   <td>逻辑与</td>
   <td><code>&amp;&amp;</code></td>
  </tr>
  <tr>
   <td>逻辑或</td>
   <td><code>||</code></td>
  </tr>
 </tbody>
</table>

### 综合使用逻辑操作符
之前说过 JavaScript 表达式在求值得时候会先处理优先级高的操作符，然后再处理算优先级低的操作符。下面代码模仿了 JavaScript 在处理逻辑表达式时内部的求值过程。

例一，求表达式 `true || !true && false` 的返回值：

```javascript
// 例一原式
true || !true && false; // 因为 ! 的优先级最高，得到下式

// 先将 !true 转化为 false
true || false && false;  // 因为 && 的优先级高于 || 得到下式

// 再将 false && false 转化为 false
true || false;

// 最后将 true || false 转化为 true
true; // 最后结果
```

例二，求表达式 `false || !true || false && true && false` 的返回值：

```javascript
// 例二原式
false || !true || false && true && false; // 因为 ! 的优先级最高，得到下式

// 先将 !true 转化为 false
false || false || false && true && false; // 因为 && 的优先级高于 || 得到下式

// 再将 false && true && false 转化为 false
false || false || false;

// 最后将 false || false || false 转化为 false
false; // 最后结果
```
例三，求表达式 `!false || true && false && !false || true && false || true || true` 的返回值：

```javascript
// 例三原式
!false || true && false && !false || true && false || true || true; // 因为 ! 的优先级最高，得到下式

// 先将原式中的两个 !false 转化为 true
true || true && false && true || true && false || true || true; // 因为 && 的优先级高于 || 得到下式

// 然后处理括号标示的内容
// true || 【true && false && true】|| 【true && false】 || true || true;
true || false || false || true || true;

// 最后将 true || false || false || true || true 转化为 true
true; // 最后结果
```

<br>
逻辑表达式中也可以用`()`操作符改变运算顺序，例如：

```javascript
var a = !false || true && true;
console.log(a); // true

// 括号中的内容被提前求值了
var b = !(false || true) && true;
console.log(b); // false
```
## 关系操作符
当我们要对数据进行比较时，就会使用 JavaScript 提供的关系操作符。 JavaScript 为我们提供了 `>`(逻辑大于)、 `<` （逻辑小于）、`>=`（逻辑大于等于）、`<=` （逻辑小于等于）、 `==`（模糊逻辑等价）、`===`（逻辑等价）、`!=`（模糊逻辑不等价）、`!==`（逻辑不等价）等等的关系操作符，下文将逐个介绍这些操作符。关系操作符常和逻辑操作符联合使用进行逻辑运算。记住，所有逻辑运算的结果都是布尔类型的数据。

### 逻辑大于和逻辑小于
`>` (逻辑大于) 和 `<`（逻辑小于）操作符让我们可以比较数据的大小。它们和数学中的 $$>$$（大于号）和 $$<$$（小于号）长得类似，但含义不同。 `>` 和 `<` 用来组成逻辑表达式或者语句，例如：

```javascript
1 < 2;
1 > 2;
```

<br>
上边的代码通过 `1 > 2` 和 `1 < 2` 描述了下列命题：
$$p: 1 小于 2$$
$$q: 1 大于 2$$

命题是有结果的，这个结果要么为真要么为假，而 JavaScript 逻辑表达式会返回相应的布尔类型数据，真命题返回`true`，假命题返回`false`。我们知道 $$p$$ 为真命题，而 $$q$$ 为假命题，所以我们能输出下列结果：

```javascript
console.log(1 < 2); // true
console.log(1 > 2); // false
```


<br>
类似的 JavaScript 还提供了 `<=`（逻辑小于等于） 和 `>=`（逻辑大于等于） 来帮助我们描述形如 $$p大于等于q$$ 和 $$p小于等于q$$ 类似的命题。例如：

```javascript
console.log(2 < 2);  // false
console.log(2 <= 2); // true
console.log(2 > 2);  // false
console.log(2 >= 2); // true
```


### 逻辑等价和逻辑不等价

当我们要用 JavaScript 描述诸如 $$p就是q$$ 或 $$p等于q$$ 等命题的时候，我们就会用到 `===` （逻辑等价操作符），例如：

```javascript
console.log(1 === 1); // true
console.log('你好' === '你好'); // true
console.log(true === 1 < 2); // true
console.log(true === 1 > 2); // false
```

在 JavaScript 中只有在值和类型都一致时才算做逻辑等价，例如：

```javascript
console.log(1 === 2); // false
console.log(1 === '1'); // false
console.log('1' === '1'); // true
console.log('1' === '2'); // false
```

<br>
同样的，如果我们希望用 JavaScript 描述 $$p不是q$$ 或者 $$p不等于q$$ 等命题，我们就会用到 `!==`（逻辑不等价操作符），`!==` 的结果刚好和 `===` 相反，例如：

```javascript
console.log(1 !== 1); // false
console.log('你好' !== '你好'); // false
```


<br>
同时 JavaScript 还提供了模糊的逻辑等价操作符 `==` 以及模糊的逻辑不等价操作符 `!=`，它们的用法和`===`、`!==`相同，但这两个操作符经常会导致非预期的结果，被许多开发者诟病，除非你非常有把握，否则不推荐使用 `==` 或者 `!=` ，这里不多介绍它们，下面举例几个费解的地方。

```javascript
console.log(1 == '1'); // true
console.log(0 == ''); // true
console.log('' == false); // true
console.log(1 == true); // true
console.log(2 == true); // false

// != 的结果与 == 相反
console.log(1 != '1'); // false
console.log(0 != ''); // false
```

## 综合使用逻辑操作符和关系操作符
综合使用逻辑操作符和关系操作符描述复合命题，这在实际开发中是非常有用的，因为我们常常要判断某些复合命题为真或是为假，例如:

$$账户名格式合法，并且密码正确，并且验证码正确。$$ （如果该命题为真，就允许登陆，为假就提示出错）
$$用户性别为女，并且年龄小于三十岁，并且有正当职业。$$ （如果该命题为真，就推送广告，为假就不推送）
$$用户输入的账户名要么是电话号码，要么是邮箱号码，要么是QQ号。$$ （如果该命题为真，就允许注册，为假就提示错误）

等等等等，这构成了程序逻辑中重要的一部分。

### 本节各个操作符的优先级总结
本节介绍了非常多的运算符，这些运算符的规则不仅在 JavaScript 中如此，它们遵循着数学的规律，因而在许多编程语言中它们的符号虽然有可能不一致，但作用是相差无几的。我们在综合使用这些运算符的时候，往往要关注它们的优先级，总体来说比较操作符的优先级高于逻辑操作符，总结如下表：

<table>
 <thead>
  <tr>
   <td>操作符类型</td>
   <td>操作符优先级</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>括号</td>
   <td><code>()</code></td>
  </tr>
  <tr>
   <td>逻辑非</td>
   <td><code>!</code></td>
  </tr>
  <tr>
   <td>关系操作符</td>
   <td><code>&lt; &lt;= &gt; &gt;= </code></td>
  </tr>
  <tr>
   <td>逻辑等价</td>
   <td><code>== != === !==</code></td>
  </tr>
  <tr>
   <td>逻辑与</td>
   <td><code>&amp;&amp;</code></td>
  </tr>
  <tr>
   <td>逻辑或</td>
   <td><code>||</code></td>
  </tr>
 </tbody>
</table>

### 逻辑表达式的求值过程
下面代码模仿了 JavaScript 在处理逻辑表达式时内部的求值过程。

例一，（a）：用 JavaScript 语句描述命题 $$age 小于 30，并且 age 大于 20$$ 。（b）：当 `age = 25` 时给出求值过程。（c）：当`age = 100` 时给出求值过程。 

* （a）

  ```javascript
  age < 30 && age > 20;
  ```
* （b）下列代码框描述的是求值过程

 ```javascript
 // 原式
 age < 30 && age > 20;
 
 // 因为关系运算符的优先级大于逻辑运算符
 // 所以先处理 age < 30 和 age > 20 
 // 因为 age 的值是25， 所以 age < 30 为 true 而 age > 20 为 true 得下式
 true && true;
 
 // 最后处理 true && true 得结果
 true; // 结果
 ```
* （c）下列代码框描述的是求值过程

 ```javascript
 // 原式
 age < 30 && age > 20;
 
 // 因为关系运算符的优先级大于逻辑运算符
 // 所以先处理 age < 30 和 age > 20 
 // 因为 age 的值是 100， 所以 age < 30 为 false 而 age > 20 为 true
 false && true;
 
 // 最后处理 false && true 得结果
 false; // 结果 
 ```
 
<br>
例二，（a）：用 JavaScript 语句描述命题 $$她的名字要么是小柳，要么是柳柳$$ (用变量名 `herName`指代 “她的名字”)。（b）：当 `herName = '小柳'` 时给出求值过程。 

 * （a）

  ```javascript
  herName === '小柳' || herName === '柳柳';
  ```
 * （b）下列代码框描述的是求值过程

 ```javascript
 // 原式
 herName === '小柳' || herName === '柳柳';
 
 // 因为关系运算符的优先级大于逻辑运算符
 // 所以先处理 herName === '小柳' 和 herName === '柳柳'
 // 因为 herName 的值是 '小柳'， 所以 herName === '小柳' 为 true 而 herName === '柳柳' 为 false 得下式
 true || false;
 
 // 最后处理 true || false 得结果
 true; // 结果
 ``` 
 
<br>
例三，给出下列表达式在 `herName = '小柳'``age = 28`时的求值过程。
  
 ```javascript
 !(herName !== '小柳') && age < 30 && age > 25 || herName === '柳柳' && age < 25 && age > 20
 ```
下面是求值过程：
 
 ```javascript
 // 原式
 !(herName !== '小柳') && age < 30 && age > 25 || herName === '柳柳' && age < 25 && age > 20;
 
 // 括号的优先级最高，先处理括号中的内容，将 herName !== '小柳' 转为 false
 !false && age < 30 && age > 25 || herName === '柳柳' && age < 25 && age > 20;
 
 // 现在是 ! 的优先级最高所以将 !false 转为 true
 true && age < 30 && age > 25 || herName === '柳柳' && age < 25 && age > 20;
 
 // 现在是 === 的优先级最高所以将 herName === '柳柳' 转化为 false
 true && age < 30 && age > 25 || false && age < 25 && age > 20;
 
 // 现在是 < 和 > 的优先级最高，所以开始处理 age < 30 、age > 25 、age < 25 、age > 20 
 // 分别转化为 true、true、false、true
 true && true && true || false && false && true;
 
 // 现在是 && 的优先级最高了，所以开始处理 true && true && true 和 false && false && true
 // 它们分别为 true、 false
 true || false;
 
 // 最后处理 true || false 得结果
 true;
 ```
 
## 逻辑运算练习题
1. 阅读下列代码，给出各个变量的值。

 ``` javascript
 var a = !true;
 var b = true || false;
 var c = false && true;
 var d = true || false && true;
 var e = true && ! false || true;
 var f = !!false;
 var g = true && !!false || !false;
 var h = !(false && false && false) && false;
 var i = !(!!true);
 ```
 
2. 阅读下列代码给出各个变量的值。

 ```javascript
 var a = 1 < 2 === true;
 var b = 2 >= 2 === true === 1 <= 2;
 var c = 1 === true;
 var d = 123 === '123';
 var e = 1 !== 1 < 2;
 var f = false !== 5 < 2;
 ```
 
3. 使用 JavaScript 语句描述下列各个命题。
 * a. age 大于等于 20 小于等于 30，并且 gender 等于 ‘女’。
 * b. 要么 age 小于 30 ，要么 age 大于 50， 并且 gender 不等于 ‘女’。
 * c. age 不在 20 和 30 之间，并且 age 不大于 80 ，并且 age 不等于 70。
 * d. username 不为‘小柳’ 或者 username 不为‘柳柳’。
 * e. type 要么为‘cellphone’，要么为‘email’。

4. 给出下列各`result`的值。
 a. 
 
 ```javascript
 var username = '柳柳', age = 26;
 var result = !(age >= 30) && !(age <= 20) && username === '小柳';
 ```
 
 b. 
 
 ```javascript
 var filmname = '日瓦戈医生', year = 1965, country = 'Czekh';
 var result = country === 'Czekh' || 
         country === 'Česká' && 
         year >= 1960 && 
         year <= 1980 && 
         filmname === '日瓦戈医生';
 ```
 
 c. 
 
 ```javascript
 var filmname = '重庆森林', year = 1994, country = 'British Hong Kong';
 var result = country === 'Hong Kong' ||
         country === 'British Hong Kong' && 
         year >= 1960 && 
         year <= 1980 && 
         filmname === '重庆森林';
 ```
  
5. 阅读代码，给出下列变量 `a~g` 的值。

 ```javascript
 var str1 = '每天你都有机会和很多人擦身而过，而你或者对他们一无所知',
     a = str1.slice(4, 12).length < 15;
 
 var num1 = (3*3 + 4*4) % 4,
     b = num1 === 0;
     
 var str2 = '13365689332',
     c = str2.slice(0, 3) === '131' ||
         str2.slice(0, 3) === '133' ||
         str2.slice(0, 3) === '135' ||
         str2.slice(0, 3) === '137' &&
         str2.length === 11;
 
 var str3 = 'Qq' + 26412314325,
     d = str3[0] === 'q' || 'Q' && str3[1] === 'q' || 'Q' && str3.length < 32;
     
 var num2 = 32872391428740479,
     e = num2 % 2 === 0;
     
 var num3 = 12345,
     f = num3.length === 5;
     
 var str4 = '不知道从什么时候开始，' +
            '在什么东西上面都有个日期，' +
            '秋刀鱼会过期，肉罐头会过期，' +
            '连保鲜纸都会过期，' +
            '我开始怀疑，' +
            '在这个世界上，' +
            '还有什么东西是不会过期的？',
     g = str4.length > 5 && 
         str4[str4.length - 1] === '的' && 
         str4.slice(str4.length - 5) === '会过期的？';
 ```
