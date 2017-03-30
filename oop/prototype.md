## 实例间共享属性的需求

前一章中我们留下了一个很重要的问题，就是如何在各个实例间共享某些属性。比如之前说道的`Circle`函数，使用它创建的每个实例中都带有一个`toString`方法，而各个实例中的`toString`方法功能是一模一样的，我们应该在让各个实例共享同一个方法，而不是每个实例都自带一个。

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

## prototype 属性

要解决上述问题，就需要使用到函数的`prototype`属性，这个属性是个对象，称之为**原型对象**，它就是 JavaScript 面向对象编程的灵魂。任何函数都有一个原型对象，它是在函数一被创建出来就存在了的。而原型对象一开始就有`constructor`属性，该属性的值是函数本身。

```javascript
var func = function () {};

// 函数一出生就有 prototype 属性
console.log(func.prototype); // {constructor: func}

// prototype 对象一出生就带有 constructor 属性
// 该属性的值是 func 函数本身
console.log(func.prototype.constructor === func); // true


// 前面代码中的 Circle 函数也是如此
console.log(Circle.prototype); // {constructor: Circle}
console.log(Circle.prototype.constructor === Circle); // true
```
> 在 JavaScript 里，数组、字符串甚至是数字都能够像对象一样通过成员操作符访问到其中的属性，那么函数也可以这么做就没什么奇怪的了。

JavaScript 中的东西一出生就带上某些玩意儿已经不是什么稀奇的事情了，比如数组和字符串一开始就有`length`，但是函数的`prototype`属性既然能够成为面向对象编程的灵魂，自然有过人之处。那就是当我们通过`new`操作符调用一个构造函数的时候`prototype`属性上的内容可以给所有这个构造函数创建出来的实例访问到。

```javascript
var a = new Circle(1,2,3);
var b = new Circle(1,2,3);

// Circle.prototype 中自带的 constructor 属性被实例 a 和 b 都访问到了
console.log(a.constructor === Circle); // true
console.log(b.constructor === Circle); // true
```

实例不仅仅能够访问到其构造函数中`prototype`里的内容，更重要的是`prototype`中的内容是由全部实例共享的。

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
// 原来的 toString 方法是 a 和 b 各有一份
console.log(a.toString === b.toString); // false
```

不仅仅是方法，属性也是可以通过这种方式共享的。

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
> `this`的具体行为会在往后讲解，一般而言，如果我们没有对某个方法做特殊处理（往后会讲解如何特殊处理），那么当我们以`对象.方法名()`的形式调用某个方法时，此时方法里的`this`指的就是这个「对象」。

## 对象自身属性和原型属性

## 动态添加和删除实例共享属性

### prototype 的动态特性

### 通过实例寻找原型 

## 总结

下一章，原型继承。