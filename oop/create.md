## 面向对象编程

一个大型程序，往往都是由多个文件，多个模块，在多人协作下完成的。想象一下一个网站，它有多个页面，每个页面有许多的按钮、输入框以及下拉菜单等等控件，每个控件长得都不一样，并且它们都可以被用户操作，每次在用户操作后都有不一样的反馈。我们想要写程序描述这一整个网站的从头到尾的运作过程太复杂了，就算是多人协作也无从下手。

先人们为了解决这种难题，就将一个网站分成了许多部分，每个控件都被他们抽象为了一个对象，通过给对象添加属性来描述这个控件的外观、位置等属性，通过给对象添加方法来描述控件的行为。如此一来，开发团队的每个人都负责几个控件，最后将他们组织起来，就能成为一个网站，这种解决问题的思想，就是面向对象的细想，以这种思想为基础编码解决问题，就叫面向对象编程。

## 批量创建对象的需求

在 JavaScript 中我们通常会按照如下方法创建一个对象，例如下面代码声明了一个`circle`对象，描述二维平面中的一个圆。

```javascript
var circle = {
  x: 12,
  y: 55,
  radius: 1,
  toString: function () {
    return 'x: ' + this.x + 
           ', y: ' + this.y;
  },
};
console.log(point.toString());
```

当对象少的时候，这样创建对象言简意赅。而一个面向对象编程的程序里，往往会有许许多多的对象，现在想象一下我们正在使用程序绘图，图像中有 20 个圆，每个圆的位置和大小不同（即`x, y, radius`的值不同），但是`toString`方法的逻辑是一样的。当使用上边的方法创造多个对象时，是不是代码开始变得有点儿恶心了呢，我们需要重复写很多的`{}`，同时要写很多的`x:` `y:` `radius: `。不仅如此，每个`circle`中都有一个一模一样的`toString`方法，当`toString`的逻辑有变动的时候，每个`circle`中的代码都要修改一轮。

因此，我们需要能够批量创建对象的方法。在传统的面向对象编程语言中（例如 Java），会先创建一个**类**，这个类就像是对象的模子，然后根据这个模子创建对象，这个过程叫**实例化**。与众不同的是 JavaScript 中没有类的概念，用它来实现面向对象思想需要使用它自己的一套方法。在详细的介绍 JavaScript 面向对象编程之前，我们先看看批量创建对象的两种常用方法。
> 在 ES6 中已经加入了 `class` 关键字可以让我们直接创建一个类。如此一来在 JavaScript 里我们也可以使用传统面向对象语言的方式来实现面向对象编程相关的方法。

## 工厂函数

当情况比较简单的时候，我们可以使用**工厂函数**批量创建对象，所谓工厂函数就是一个返回对象的函数，其内容就是配置这个对象的逻辑。例如下边代码中的`createCircle`函数就是一个可以批量创建`circle`对象的函数。

```javascript
// 批量创建 circle 对象
var createCircle = function (x, y, radius) {
  var circle = {
    x: x,
    y: y,
    radius: radius,
    toString: function () {
      return 'x: ' + this.x + ', y: ' + this.y;
    },
  };  
  return circle;
}

var a = createCircle(1,2,3);
var b = createCircle(4,5,6);

console.log(a.toString()); // x: 1, y: 2
console.log(b.toString()); // x: 4, y: 5
```

这种创建批量创建对象的方式简单好用，适合用作当批量创建的对象的作用比较单一的情况，最典型的情况就是创建的**对象只用来记录某些数据**，例如下面的`book`对象，它只记录了书本的信息。

```javascript
var createBook = function (title, author, years) {
  var book = {};
  book.title = title;
  book.author = author;
  book.years = years;
  return book;
}
```

但如果情况复杂，那么工厂函数就有如下缺点：

1. 无法通过对象实例判断对象的来源。
2. 对象中没法共用一些属性或方法。

如果项目规模宏大，第一个缺点会造成团队协作的困难，第二个缺点会造成巨大的内存浪费。例如我们之前定义的`createCircle`函数，就表现出了上述缺点，如下代码描述：

```javascript
var a = createCircle(1,2,3);
var b = createCircle(4,5,6);

// 缺点一的体现：
// 我们无法完成下列 if 语句中的判断条件
if (/* a 和 b 都是通过 createCircle 创建的对象*/) {
  // 一些逻辑
}


// 缺点二的体现：
// a 和 b 中的 toString 是两个函数，我们应该让 a 和 b 共用同一个函数
// 否则当我们使用 createCircle 创建了 10000 个对象的时候
// 就会有 10000 个一模一样的 toString 方法，这对内存是巨大的浪费

// a 和 b 都有 toString 函数，他们各自的 toString 函数的逻辑是一样的
console.log(a.toString()); // 'x: 1, y: 2'
console.log(b.toString()); // 'x: 4, y: 5'

// 我们修改了 a.toString 但 b.toString 不受任何影响
// 这说明他们没有共用一个函数
a.toString = function () {
  return 'a';
}
console.log(a.toString()); // 'a'
console.log(b.toString()); // 'x: 4, y: 5'
```

因此，当批量创建的对象情况比较复杂的时候，我们就需要其他批量创建对象的方式了，接下来这种创建对象的方式，是使用 JavaScript 实现面向对象思想的基础，它就是**构造函数**。

## 构造函数

现在我们将上文的 `createCircle` 工厂函数改写为构造函数的形式。

```javascript
var Circle = function (x, y, radius) {
  this.x = x;
  this.y = y;
  this.radius = radius;
  this.toString = function () {
    return 'x: ' + this.x + ', y: ' + this.y;
  };
}

var a = new Circle(1,2,3);
var b = new Circle(4,5,6);

console.log(a.toString()); // x: 1, y: 2
console.log(b.toString()); // x: 4, y: 5
```
> 根据编程中的传统规范，构造函数使用大写字母开头，当你使用大写字母开头了，别人就懂这是构造函数了。

我们通过`new Circle(...)`的形式使用构造函数，就能得到一个新的对象了，当你在控制台上输出通过构造函数创建的对象的时候，控制台会告诉你它的来源。

```javascript
var a = createCircle(1,2,3);
var b = new Circle(4,5,6);

console.log(a); // object
console.log(b); // Circle
```

通过构造函数创建的对象，叫做这个构造函数的**实例**，例如上边代码中的`b`就是构造函数`Circle`的实例，在编程中我们只需对实例使用 `instanceof` 操作符，就能在编程中判断某个实例的来源了。

```javascript
var b = new Circle(4,5,6);
b instanceof Circle; // true
```

构造函数一开始就解决了工厂函数中「无法通过对象实例判断对象的来源」这个缺点。

未完待续...
