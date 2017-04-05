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

要解决上述问题，就需要使用到函数的`prototype`属性，这个属性的值是个对象，称之为**原型对象**，它就是 JavaScript 面向对象编程的灵魂。任何函数都有一个原型对象，它是在函数一被创建出来就存在了的。而原型对象一开始就有`constructor`属性，该属性的值是函数本身。

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

// Circle.prototype 中压根儿就没有 toString 方法
console.log(Circle.prototype.toString); // undefined
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

// 访问实例 a 原型上的属性
console.log(a.name); // '柳柳'

// 给实例 a 自身加上 name 属性
// 现在实例 a 和它的原型上都有 name 属性
a.name = '沫沫';

// 此时我们访问到的就是实例 a 自身的属性了
console.log(a.name); // '沫沫'

// 当然原型上的 name 属性还在
console.log(NullObject.prototype.name); // '柳柳'

// 它依然能够发挥它原有的作用
var b = new NullObject();
console.log(b.name); // '柳柳'

// 我们删除实例 a 自身的 name 属性以后
// 就又可以访问到原型上的 name 属性了
delete a.name;
console.log(a.name); // '柳柳'
```

如果我们想要判断某个属性是否存在于某个实例自身或是其原型上时就可以使用`in`操作符，例如：

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
>   if (key === 'name') {
>     console.log(key); // name
>   }
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

// gender 属性不在原型上也不在实例自身，返回 false
console.log(a.hasOwnProperty('gender')); // false
```


... 未完待续

## 找到实例的原型 

## 原型的动态特性

## 总结
