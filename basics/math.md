## Math 对象

通常情况下，我们通过编码来处理一些数学任务是比较繁琐的，就算是一些简单的数学任务也是如此，但是有些数学任务是非常常见的，因而许多编程语言都会提供一个专门用来处理一些简单数学任务的模块。在 JavaScript 中，这个模块就是 `Math` 对象。这个对象中有许多数学方法和数学常量，这里介绍其中比较常用的几个方法和常量。

## Math 对象中的数学常量

`Math`是一个对象，我们可以直接使用成员操作符访问到其中的属性。有的属性是方法，有的属性是常量，作为常量的属性中，有两个是我们熟悉并且常见的，那就是圆周率 $$\pi$$ 和自然对数的底数 $$e$$。

我们可以通过`Math.PI`访问到 $$\pi$$，通过`math.E`访问到 $$e$$ 的近似值。

```javascript
console.log(Math.PI); // 3.141592653589793
console.log(Math.E);  // 2.718281828459045
```

## Math 对象中的常用方法

通过 `Math` 对象提供了许多处理数学任务的方法可以减轻我们的负担。下面介绍`Math`中常用的几个方法。

### 最大最小值

在前面几章的练习中，有些习题需要求找到一个序列的最大值或者最小值，当时我们会通过组合条件语句和迭代语句编码完成试题。实际上`Math`对象中的`max`和`min`方法也能得到一个序列的最大值或是最小值，而且只用一行代码就实现了。

```javascript
var max = Math.max(2,3,4,5,6,7);
console.log(max); // 7

var min = Math.min(2,3,4,5,6,7);
console.log(min); // 2
```

这个序列可长可短。

```javascript
var max = Math.max(2,3,4,7);
console.log(max); // 7

var min = Math.min(3,4);
console.log(min); // 3
```

如果我们想从某个数组中找到它的最大最小值，我们可以通过如下方法使用`Math.max`或是`Math.min`。

```javascript
var max = Math.max.apply(null, [2,3,4,5,6,7]);
console.log(max); // 7

var min = Math.min.apply(null, [2,3,4,5,6,7]);
console.log(min); // 2
```
> apply 的具体功能会在会在本书的第三部分介绍，现阶段只需记住可以这么使用就好。

### 取整

`Math`对象中提供了三个方法可以让我们以不同的方式对数字取整，他们分别是：

1. `Math.round` 四舍五入
2. `Math.floor` 向下取整
3. `Math.ceil` 向上取整

这三个方法都接受一个数字作为参数，返回取整后的整数。

```javascript
// 四舍五入
console.log(Math.round(1.4)); // 1
console.log(Math.round(1.5)); // 2

// 向下取整
console.log(Math.floor(1)); // 1
console.log(Math.floor(1.4)); // 1
console.log(Math.floor(1.5)); // 1
console.log(Math.floor(1.999999)); // 1

// 向上取整
console.log(Math.ceil(1)); // 1
console.log(Math.ceil(1.4)); // 2
console.log(Math.ceil(1.5)); // 2
console.log(Math.ceil(1.000001)); // 2
```

## 随机数

`Math.random`方法可以得到一个在区间 $$[0,1]$$ 上的随机数，这个方法没有参数。

```javascript
console.log(Math.random()); // 0.7513179241936767
console.log(Math.random()); // 0.14205328961588592
console.log(Math.random()); // 0.968618524049834
```
> 既然是随机数，那么每次调用的结果会都不一样。

`Math.random`产生的随机数，并不是数学意义上的随机，它是通过算法生成的，不同浏览器实现的随机算法不一样。

有的时候，我们并不需要 $$[0,1]$$ 区间上的随机数，想要 $$[0, 100]$$ 区间上的，此时我们就可以给通过给`Math.random`的结果乘以`100`来得到我们想要的结果。

```javascript
console.log(Math.random() * 100); // 84.40268700798883
console.log(Math.random() * 100); // 82.56584363637411
console.log(Math.random() * 100); // 37.03991930486852
```

嫌小数恶心，希望得到的是区间 $$[0, 100]$$ 上的整数？此时就可以使用我们刚学的`Math.round`来进行取整。

```javascript
console.log(Math.round(Math.random() * 100)); // 83
console.log(Math.round(Math.random() * 100)); // 51
console.log(Math.round(Math.random() * 100)); // 92
```

组合使用`Math.random`和`Math.round`可以生成各种区间里的随机数。

### 幂运算

之前的学习中，当我们要对变量`a`进行幂运算的时候都是将这个变量自乘，例如计算`a`的平方使用`a * a`。此种操作方式在幂次较低的时候是没问题的，但是如果我们想要计算`a`的 8 次幂，或者 32 次幂的时候，将变量自乘的做法就显得有点繁琐了，此时我们就可以使用`Math.pow`方法，这个方法接受两个参数，第一个参数是基数，第二个参数是指数。下列代码代码计算了 $$2^{21}$$ 和 $$a^9$$。

```javascript
var a = 10;

console.log(Math.pow(2, 21)); // 2097152
console.log(Math.pow(a, 9));  // 1000000000
```

指数也能是分数，因此我们可以通过将指数设置为`1/n`来计算 $$\sqrt[n]{x}$$ 的结果，例如，设置为`1/2`可以得到 $$\sqrt{x}$$ 的结果，设置为`1/3`可以得到 $$\sqrt[3]{x}$$ 的结果。

```javascript
console.log(Math.pow(4, 1/2)); // 2
console.log(Math.pow(27, 1/3)); // 3
```

求平方根是一个很常用的功能，为此`Math`中专门有一个`sqrt`方法给我们使用。`Math.sqrt(x)`的结果和`Math.pow(x, 1/2)`的结果一致。

```javascript
console.log(Math.sqrt(64)); // 8
console.log(Math.sqrt(49)); // 7
```

## Math 对象练习

1. 编码求序列`32,546,21,46,5,343,23`的最大值和最小值。
2. 编码求数组`[3235,54,546,45,34,235,36,53,34234,36,6,45,5]`中最大的成员和最小的成员。
3. 将数学常数 $$\pi$$ 和 $$e$$ 分别向上取整，向下取整，和四舍五入。
4. 生成在区间 $$[0, 10]$$ 上的随机整数。
5. 生成在区间 $$[10, 20]$$ 上的随机整数。
6. 求 $$2^{22}$$ 和 $$3^{11}$$ 的值。
7. 求 $$\sqrt{100}$$ 和 $$\sqrt[5]{10000}$$ 的近似值。