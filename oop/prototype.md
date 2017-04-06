## 实例间共享属性的需求

前一章中留下了一个很重要的问题，就是如何在各个实例间共享某些属性。比如之前说道的`Circle`函数，使用它创建的每个实例中都带有一个`toString`方法，而各个实例中的`toString`方法功能是一模一样的，我们应该在让各个实例共享同一个方法，而不是每个实例都自带一个。

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
    return new Circle(x, y, radius);
  }
}

var a = new Circle(1,2,3);
var b = new Circle(4,5,6);

// a 和 b 各持有一份 toString 函数，这两份 toString 函数的功能是一样的
console.log(a.toString()); // 'x: 1, y: 2'
console.log(b.toString()); // 'x: 4, y: 5'

// 虽然功能一样，但它们毕竟不是同一个函数
console.log(a.toString === b.toString); // false
```

## 构造函数的 prototype 对象

要解决上述问题，就需要使用到函数的`prototype`属性，这个属性的值是个对象，它就是 JavaScript 面向对象编程的灵魂。任何函数都有一个`prototype`属性，它是在函数一被创建出来就存在了的。而`prototype`对象一开始就有`constructor`属性，该属性的值是函数本身。

```javascript
// 创建一个函数
var func = function () {};

// 该函数一出生就有 prototype 属性
console.log(func.prototype); // {constructor: func}

// prototype 对象一出生就带有 constructor 属性
// 该属性的值是 func 函数本身
console.log(func.prototype.constructor === func); // true


// 前面代码中的 Circle 函数也是如此
console.log(Circle.prototype); // {constructor: Circle}
console.log(Circle.prototype.constructor === Circle); // true
```

JavaScript 中的东西一出生就带上某些玩意儿已经不是什么稀奇的事情了，比如数组和字符串一开始就有`length`属性，但是函数的`prototype`属性能够成为这门语言面向对象编程的灵魂自然有过人之处。那就是当我们通过`new`操作符调用一个构造函数的时候，这个构造函数`prototype`属性上的内容可以让所有这个构造函数创建出来的实例访问到。

```javascript
var a = new Circle(1,2,3);
var b = new Circle(1,2,3);

// Circle.prototype 中自带的 constructor 属性被实例 a 和 b 都访问到了
console.log(a.constructor === Circle); // true
console.log(b.constructor === Circle); // true
```

某个实例的**原型**，就是其构造函数的`prototype`属性。例如上边代码中的`Circle.prototype`就是实例`a`和`b`的**原型**。实例不仅仅能够访问到其原型中的内容，更重要的是，其原型中的内容是由全部实例共享的。

```javascript
// 在 Circle.prototype 中添加 func 方法
Circle.prototype.func = function () {
  return 'circle';
};

// 然后 Circle 的实例就带有了 func 方法。
var a = new Circle(1,2,3);
var b = new Circle(1,2,3);
console.log(a.func()); // 'circle'
console.log(b.func()); // 'circle'

// 不仅如此，a 和 b 共享同一份 func 方法
console.log(a.func === b.func); // true

// 他们共享的的那份 func 方法来自 Circle.prototype.func
console.log(a.func === Circle.prototype.func); // true
console.log(b.func === Circle.prototype.func); // true

// 而原来的 toString 方法则不是，
// 原来的 toString 方法是 a 和 b 中各有一份
console.log(a.toString === b.toString); // false
```

不仅仅是函数，其他类型的属性也可以通过这种方式共享。

```javascript
Circle.prototype.name = 'circle';

// 然后 Circle 的实例就带有了 name 属性。
var a = new Circle(1,2,3);
var b = new Circle(1,2,3);
console.log(a.name); // 'circle'
console.log(b.name); // 'circle'
```

如此一来，我们希望`Circle`的各个实例共享`toString`方法，我们只需将该方法放置到`Circle.prototype`中就可以。

```javascript
var Circle = function (x, y, radius) {
  if (this instanceof Circle) {
    this.x = x;
    this.y = y;
    this.radius = radius;
  } else {
    return new Circle(x, y, radius);
  }
}
Circle.prototype.toString = function () {
  return 'x: ' + this.x + ', y: ' + this.y;
}

var a = new Circle(1,2,3);
var b = new Circle(4,5,6);

// 别忘了，当我们以 a.toString() 的形式调用的时候
// Circle.prototype.toString 中的 this 指的就是当前对象
console.log(a.toString()); // 'x: 1, y: 2'
console.log(b.toString()); // 'x: 4, y: 5'
```
> 再次提示，当我们使用`某对象.方法()`的形式调用某个方法时，此时方法里的`this`指的就是这个「某对象」自身。例如上边代码中`Circle.prototype.toString`函数体中的`this`，以`a.toString()`的形式调用时它就是实例`a`，以`b.toString()`的形式调用时它就是实例`b`，`this`相关知识往后专门讲解。

## 实例自身属性和原型属性

既然我们可以同时访问到实例自身和它原型上的属性，那么就可能会遇到这么一个问题，那就是实例自身的属性和原型中的属性同名，此时我们通过成员操作符访问实例的属性时，会得到实例自身的属性，例如：

```javascript
// NullObject 构造函数创建的实例是一个空对象
var NullObject = function () {}

// 原型上有个 name 属性
NullObject.prototype.name = '柳柳';

var a = new NullObject();

// a.name 访问到的是实例 a 原型（也就是 NullObject.prototype）上的属性
console.log(a.name); // '柳柳'

// 给实例 a 自身加上 name 属性
// 现在实例 a 和它的原型上都有 name 属性
a.name = '沫沫';

// 此时 a.name 访问到的就是实例 a 自身的属性
console.log(a.name); // '沫沫'

// 当然原型上的 name 属性还在
console.log(NullObject.prototype.name); // '柳柳'

// 它依然能够发挥它原有的作用
var b = new NullObject();
console.log(b.name); // '柳柳'

// 我们删除实例 a 自身的 name 属性以后
// a.name 访问到的又是原型上的 name 属性了
delete a.name;
console.log(a.name); // '柳柳'
```

如果我们想要判断某个属性是否存在于某个实例自身或是其原型上时可以使用`in`操作符，例如：

```javascript
var NullObject = function () {}
NullObject.prototype.name = '柳柳';

var a = new NullObject();

// 在原型上返回 true
console.log('name' in a); // true;

// 在实例上也返回 true
a.age = 17;
console.log('age' in a); // true;

// 不在实例上也不在原型上，返回 false
console.log('gender' in a); // false
```
> `for...in`语句中的`in`就是上文提到的`in`操作符，因为`in`操作符的这种特性，所以当我们使用`for...in`迭代对象的时候，会访问到对象原型上的属性，例如:
> 
> ```javascript
> var NullObject = function () {}
> NullObject.prototype.name = '柳柳';
>
> var a = new NullObject();
> a.age = 17;
> 
> for (var key in a) {
>   console.log(key); // 不仅会输出 'age' 还会输出 'name'
> }
> ```

当我们需要切实的知道某个属性是实例自身还是原型上的时候，就可以使用实例的`hasOwnProperty`方法，该方法的参数是个属性名，如果属性存在于这个实例自身，该方法返回`true`，否则返回`false`，例如：

```javascript
var NullObject = function () {}
NullObject.prototype.name = '柳柳';

var a = new NullObject();
a.age = 17;

// age 属性在实例自身，返回 true
console.log(a.hasOwnProperty('age')); // true

// name 属性虽然在原型上，但不在实例自身，返回 false
console.log(a.hasOwnProperty('name')); // false

// 总之只要不在实例自身，一律返回 false
console.log(a.hasOwnProperty('gender')); // false
```

有时候区分某个属性是实例自身的还是其原型上的是非常重要的，比如在现实开发中经常会有合并对象的需求，那么我们就可以实现一个`merge`函数来完成相关操作，其实现如下：

```javascript
var Info = function (age, gender) {
  this.age = age
  this.gender = gender
}
Info.prototype.run = function () {};

// 将对象 b 的属性合并到 a 中
var merge = function (a, b) {
  for (var key in b) {
    // 判断 key 是在 b 自身还是其原型上
    // 防止错误的将 b 原型上的属性合并到 a 中
    if (b.hasOwnProperty(key)) {
      a[key] = b[key];
    }
  }
  return a;
}

var a = {name: 'Lucy'};
var b = new Info(17, 'female');

merge(a, b);

// 对象 b 原型中的 run 属性没有被合并到 a 中
console.log(a); // {name: 'Lucy', age: 17, gender: 'female'}
```
> 删掉上边代码中的判断语句再试试，你就会发觉`b`原型里的`run`属性出现在了`a`中，把一个`b`对象自身没有的属性合并到了`a`中，这很不合理。

## 找到实例的原型 

某些特殊的情况下，我们需要通过实例取得它的原型。之前介绍过，每个函数的`prototype`属性都自带有一个`constructor`属性，该属性的值是函数自身。另外函数的实例可以访问到`prototype`对象中的属性，所以函数的实例可以通过`constructor.prototype`访问到它的原型。

```javascript
var NullObject = function () {}
var a = new NullObject();

console.log(a.constructor === NullObject); // true
console.log(a.constructor.prototype === NullObject.prototype); // true
```

正常情况下，通过上面代码的方式找到某个实例的原型是没问题的，除了语句长一些。但是夜路走多了总会碰到鬼，比如在多人合作的时候，某个吃瓜群众给实例自身加上了`constructor`属性并且赋值为一个字符串、再比如原型上的`constructor`的值被改动过，那么上面的代码就失效了，从而引发一些列的 bug 导致我等码农留下来加班。因此 JavaScript 提供了`Object.getPrototypeOf`方法让我们获取某个实例的原型，该方法接受一个参数，就是实例。返回值是这个实例的原型，如果这个实例没有原型，则返回`null`：

```javascript
var NullObject = function () {}
var a = new NullObject();

// Object.getPrototypeOf 可以获取实例 a 的原型
var proto = Object.getPrototypeOf(a);
console.log(proto === NullObject.prototype); // true

// 就算 a.constructor 和
// NullObject.prototype.constructor 被改动过也可以正常生效
a.constructor = 'mama';
NullObject.prototype.constructor = 'haha';
proto = Object.getPrototypeOf(a);
console.log(proto === NullObject.prototype); // true
```
> 有些代码中使用实例的`__proto__`属性来获取该实例的原型，这在大部分浏览器里是可以生效的。但是`__proto__`属性长得比较丑并且不是标准属性，所以还是推荐大家使用标准的`Object.getPrototypeOf`方法。

## 原型的动态特性

介绍了如此多实例和原型的关系，现在来说说原型的动态性。所谓动态特性，就是我们修改了某个构造函数的`prototype`属性，那么改动会实时的对这个构造函数所创建出来的实例生效，这是 JavaScript 面向对象编程中一个很有意思的地方，比如：

```javascript
var NullObject = function () {}

var a = new NullObject();
var b = new NullObject();

// 一开始实例 a 和 b 都不能访问到 name 属性
console.log(a.name, b.name); // undefined undefined

// 给原型加入 name 属性后，我们不用对 a 和 b 做任何修改
// 就能够访问到 name 属性了
NullObject.prototype.name = 'haha';
console.log(a.name, b.name); // 'haha' 'haha'
```

## 总结

在 JavaScript 中原型是个相对难懂的概念，许多书籍和文章对其的介绍都语焉不详，我本人在学习 JavaScript 的过程中也在里面绕了很久，本章介绍了原型的作用，及其和实例的关系。

总结一下就是，构造函数的`prototype`属性就是它所创建的实例的原型，原型是个对象，它其中的属性会跟所有这个构造函数创建出来的实例共享，当实例和其原型上的属性同名时，我们会首先取得实例上的属性，实例的`hasOwnProperty`方法帮助我们判断某个属性是否属于实例自身，`Object.getPrototypeOf`方法帮助我们通过实例获取它的原型，我们对原型作出改动，会立即影响到所有它的实例。

上一章是这一章的基础，这章起着承上启下的作用，下章将介绍继承和原型链，它们是 JavaScript 面向对象编程中很重要的概念，也是理解这门语言许多机制的关键。
