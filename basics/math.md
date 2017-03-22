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

### 随机数



### 幂运算

### 绝对值