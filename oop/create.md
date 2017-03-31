## 面向对象编程

一个大型程序，往往都是由多个文件，多个模块，在多人协作下完成的。想象一下一个网站，它有多个页面，每个页面有许多的按钮、输入框以及下拉菜单等等控件，每个控件长得都不一样，并且它们都可以被用户操作，每次在用户操作后都有不一样的反馈。我们想要写程序描述这一整个网站的从头到尾的运作过程太复杂了，所以应该换种思路。

先人们为了解决这种难题，就将一个网站分成了许多部分，每个控件都被他们抽象为了一个对象，通过给对象添加属性来描述这个控件的外观、位置等属性，通过给对象添加方法来描述控件的行为。如此一来，开发团队的每个人都负责几个控件，最后将他们组织起来，就能成为一个网站，这种解决问题的思想，就是面向对象的细想，以这种思想为基础编码解决问题，就叫面向对象编程。

## 批量创建对象的需求

在 JavaScript 中我们通常会按照如下方法创建一个对象，例如下面代码声明了一个`circle`对象，描述二维平面中的一个圆。

```javascript
var circle = {
  x: 12,
  y: 55,
  radius: 1,
  toString: function () {
    return 'x: ' + x + 
           ', y: ' + y;
  },
};
console.log(point.toString());
```

当对象少的时候，这样创建对象言简意赅。而一个面向对象编程的程序里，往往会有许许多多的对象，现在想象一下我们正在使用程序绘图，图像中有 20 个圆，每个圆的位置和大小不同（即`x, y, radius`的值不同），但是`toString`方法的逻辑是一样的。当使用上边的方法创造这 20 个对象时，是不是代码开始变得有点儿恶心了呢，我们需要重复写很多的`{}`，同时要写很多的`x:` `y:` `radius: `。不仅如此，每个`circle`中都有一个一模一样的`toString`方法，当`toString`的逻辑有变动的时候，每个`circle`中的代码都要修改一轮。

因此，我们需要能够批量创建对象的方法。在传统的面向对象编程语言中（例如 Java）创建对象，会先创建一个**类**，这个类就像是对象的模子，然后根据这个模子创建对象，这个过程叫**实例化**。与众不同的是 JavaScript 中没有类的概念，用它来实现面向对象思想需要使用它自己的一套方法。在详细的介绍 JavaScript 面向对象编程之前，我们先看看批量创建对象的两种常用方法。
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
      return 'x: ' + x + ', y: ' + y;
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
2. 各个对象没法共用一些属性或方法。

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
// a 和 b 各持有一份 toString 方法，这两个 toString 方法的功能是一样的
// 所以我们应该让它们共用一个函数
// 否则当我们使用 createCircle 创建了 10000 个对象的时候
// 就会有 10000 个一模一样的 toString 方法，这对内存是巨大的浪费

// a 和 b 各持有一份 toString 函数，这两份 toString 函数的功能是一样的
console.log(a.toString()); // 'x: 1, y: 2'
console.log(b.toString()); // 'x: 4, y: 5'

// 虽然功能一样，但它们毕竟不是同一个函数
console.log(a.toString === b.toString); // false
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
    return 'x: ' + x + ', y: ' + y;
  };
}

var a = new Circle(1,2,3);
var b = new Circle(4,5,6);

console.log(a.toString()); // x: 1, y: 2
console.log(b.toString()); // x: 4, y: 5
```
> 根据编程中的传统约定，构造函数使用大写字母开头，当你使用大写字母开头了，别人就懂这是构造函数了。

我们通过`new Circle(...)`的形式使用构造函数，就能得到一个新的对象了，当你在控制台上输出通过构造函数创建的对象的时候，控制台会告诉你它的来源。

```javascript
var a = createCircle(1,2,3);
var b = new Circle(4,5,6); // 注意，这里的`new`操作符不能省略。

console.log(a); // object
console.log(b); // Circle
```

通过构造函数创建的对象，叫做这个构造函数的**实例**，例如上边代码中的`b`就是构造函数`Circle`的实例，在编程中我们只需对实例使用 `instanceof` 操作符能判断它的来源。

```javascript
var isCircle = b instanceof Circle;
console.log(isCircle); // true
```

构造函数一开始就解决了工厂函数中「无法通过对象实例判断对象的来源」这个缺点。至于第二个缺点「各个对象没法共用一些属性或方法」，则需要原型相关的知识，那是下一章的内容，在进入下章之前，先深入了解下构造函数，方便加深印象和日后使用这种函数。首先，我们来看看工厂函数和构造函数的异同。

```javascript
// 构造函数
var Circle = function (x, y, radius) {
  // 将参数赋值给 this 变量
  this.x = x;
  this.y = y;
  this.radius = radius;
  this.toString = function () {
    return 'x: ' + x + ', y: ' + y;
  };
}
var a = new Circle(1,2,3); // 调用时需要使用 new 操作符

// 工厂函数
var createCircle = function (x, y, radius) {
  
  // 声明一个对象 circle，并将参数作为 circle 的属性 
  var circle = {
    x: x,
    y: y,
    radius: radius,
    toString: function () {
      return 'x: ' + x + ', y: ' + y;
    },
  };
  
  // 返回 circle
  return circle;
}
var b = createCircle(4,5,6); // 直接调用
```

对比上边的代码我们就可以看出，它们都是函数（都通过函数表达式得到）。它们的内部构造非常类似，都是根据参数给某个对象添加属性，区别是工厂函数`return`了这个变量但构造函数函数并没有。另外构造函数调用时需要使用 `new` 操作符而工厂函数不需要。

工厂函数我们已经十分熟悉了，它就是一个返回值是一个对象的普通函数。而构造函数则有点儿奇特，它没有`return`却能得到调用结果，在它的内部，我们是给一个特殊的`this`对象添加属性，调用时得加上`new`操作符。但其实，构造函数本是一个普通函数，它之所以成为构造函数，关键就是调用时的`new`操作符。比起直接调用某个函数，我们在使用`new`操作符调用函数时 JavaScript 会多做如下几件事：

1. 创建一个可以通过`instanceof`追踪到来源的对象。
2. 将这个对象赋值给函数体中的`this`变量。
3. 在函数体的代码执行完毕后返回这个新对象。

如果我们在调用`Circle`时没使用`new`操作符，那么它将与普通函数没什么区别。

```javascript
var a = Circle(1,2,3);
console.log(a); // undefined
```
因为`Circle`内部没有`return`语句，所以直接调用的结果是`undefined`，如果我们对`Circle`做出如下改造让它返回某个结果，那么我们在直接调用时就能得到这个结果，如下。

```javascript
var Circle = function (x, y, radius) {
  this.x = x;
  this.y = y;
  this.radius = radius;
  this.toString = function () {
    return 'x: ' + this.x + ', y: ' + this.y;
  };
  return 'x: ' + x + ', y: ' + y + ', radius: ' + radius; // 返回一个字符串
}

var a = Circle(1,2,3);
console.log(a); // 'x: 1, y: 2, radius: 3'

var b = new Circle(1,2,3);
console.log(b instanceof Circle); // true
```

说到这里，是不是发觉上边代码中的`Circle`函数和之前学的`Date`函数有些相似呢。其实`Date`函数就是一个典型的构造函数，用来批量创建「Date 对象」。它直接调用的结果是也一个字符串，而加上了`new`操作符以后就将得到一个「Date 对象」。

```javascript
var a = Date();
console.log(typeof a); // string

var b = new Date();
console.log(typeof b); // object
console.log(b instanceof Date); // true
```
> 如你所见，因为`Date`函数是构造函数所以它也是大写字母开头。

好了`Date`函数我们先放到一边。

在`Circle`函数的函数体中，我们给`this`变量添加了许多属性，我们知道当我们使用`new`操作符调用`Circle`函数时`this`变量会是一个新创建的、可以使用`instanceof`追踪到来源的对象。而如果当我们直接调用`Circle`时，其内部的`this`变量的值就变得非常复杂，在不同的情况下，它有可能是全局对象（全局作用域），有可能是某个不属于自己的对象，等等等等。

```javascript
var Circle = function (x, y, radius) {
  this.x = x;
  this.y = y;
  this.radius = radius;
  this.toString = function () {
    return 'x: ' + x + ', y: ' + y;
  };
  return 'x: ' + x + ', y: ' + y + ', radius: ' + radius; // 返回一个字符串
}

var a = Circle(1,2,3); // 直接调用 Circle

// 当我们直接调用 Circle 时，稀里糊涂的在全局作用域中加入了四个变量，
// 这是很危险的事情，如果全局作用域中之前有其他人的声明的变量 x 或者 y 那么原先的值就会被覆盖
console.log(x, y, radius, toString); // 1 2 3 function () {....}
```
> 上面的代码在有些浏览器中可以看到结果，这取决于浏览器运行着 JavaScript 的哪种模式。
> 运行上边代码的时候先刷新浏览器。

随着学习的推进大家会明白为什么这里的`this`会是全局作用域，总而言之，如果我们直接调用`Circle`，其内部`this`变量指代不明这种情况有可能带来许多不可预料的问题，除非你非常非常有把握，否则一定不能在调用构造函数的时候省略`new`操作符。

JavaScript 中所有内建的构造函数（如`Date`函数）都可以直接调用并且没有任何问题。有时我们希望自己写的构造函数也能如此，以避免在多人协作的时候有某个粗心的人在使用该构造函数时忘记加`new`从而给整个程序带来隐患。想要达到这种效果，可以在创建构造函数的时候通过`instanceof`操作符判断`this`的来源，如果`this`来源于当前构造函数则说明在这个构造函数在被调用时是加了`new`的，否则没加`new`，例如本章中的`Circle`可以通过如下方法改造，从而避免在没加`new`时给程序带来隐患。

```javascript
var Circle = function (x, y, radius) {
  // 如果这个 this 变量起源于 Circle 
  // 那么说明此时 Circle 在被调用时是加了 new 的
  // 可以大胆的给 this 赋值
  if (this instanceof Circle) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.toString = function () {
      return 'x: ' + x + ', y: ' + y;
    };
  } else {
    // 否则就是在调用时没加 new 
    // 直接返回字符串
    return 'x: ' + x + ', y: ' + y + ', radius: ' + radius; // 返回一个字符串
  }
}
```
> 在`Circle`函数里使用`Circle`很奇怪对不对。其实函数都是先创建再运行的，也就是说当`Circle`函数体中的代被运行时`Circle`函数早就被创建和赋值了，因此我们在函数体里就可以像访问一个全局变量一样访问到它，甚至还能调用它。

当然，在不加`new`时不一定非得返回字符串，如果希望不管这个构造函数在被调用时无论加没加`new`都返回正确的实例也是可以的，那么就需要对本章中的`Circle`进行如下改造：

```javascript
var Circle = function (x, y, radius) {
  if (this instanceof Circle) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.toString = function () {
      return 'x: ' + x + ', y: ' + y;
    };
  } else {
    // 调用构造函数时不喜欢加 new ？ 
    // 看本工程师给你强行加一个。
    return new Circle(x, y, radius);
  }
}
```

就算如此，也应该谨记，在使用构造函数时除非对不加`new`的后果非常有把握，否则一定别忘了`new`。

## 总结

不仅仅是批量创建对象，当我们要创建的对象非常复杂的时候，使用工厂函数或者构造函数创建对象也是个非常不错的选择，它们将创建对象的逻辑包裹在了函数的内部，如此一来，这个函数就可以当成一个模块，方便查找和修改。

到这里为止，我们还是没有解决工厂函数的第二个缺点，即「各个对象没法共用一些属性或方法」，在下一章中我们会开始学习 JavaScript 面向对象的灵魂——**原型**，它不仅可以解决这个问题，还可以使用它来实现更多面向对象的思想。同时**原型**也是理解 JavaScript 这门语言许多机制的基础，比如为什么字符串明明不是对象却可以用过成员操作符访问到`length`属性。

## 创建对象练习