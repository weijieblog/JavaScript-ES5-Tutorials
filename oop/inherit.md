## 原型的原型

上一章说道，某个实例的原型就是其构造函数的`prototype`属性，这个属性是一个对象。那既然原型也是一个对象，就意味着它也能够通过一个构造函数来创建，如此一来就出现了原型的构造函数，而构造函数作为函数一出生就带有`prototype`属性，那么就出现了「原型的原型」。例如下边代码中，构造函数`Dog`的实例`wangCai`，它的原型（也就是`Dog.prototype`）是通过另外一个构造函数`Animal`创建的，所以`Animal.prototype`就是实例`wangCai`原型（也就是`Dog.prototype`）的原型。

```javascript
var Animal = function () {};

var Dog = function () {};
Dog.prototype = new Animal();

var wangCai = new Dog();

console.log(wangCai instanceof Dog); // true
console.log(Dog.prototype instanceof Animal); // true
```

下图描述了上边代码中的原型关系：

```{mermaid}
graph LR
  A[wangCai] -- 的原型是 --> B[Dog.prototype]
  B[Dog.prototype] -- 的原型是 --> C[Animal.prototype]
  A[wangCai] -- 的原型的原型是 --> C[Animal.prototype]
```

如上文所述，`wangCai`是`Dog`的实例，而它的原型`Dog.prototype`，则是`Animal`的实例。我们知道一个实例不仅仅能够访问到他自身的属性，还能够访问到它原型上的属性。那么`wangCai`可以访问到它的原型`Dog.prototype`上的属性而`Dog.prototype`可以访问到`Animal.prototype`上的属性。

```{mermaid}
graph LR
  A[wangCai] -- 可以访问 --> B[Dog.prototype]
  B[Dog.prototype] -- 可以访问 --> C[Animal.prototype]
```

我们可以通过代码验证上面的观点。

```javascript
var Animal = function () {};
Animal.prototype.eat =function () {
  console.log('eating...');
};

var Dog = function () {};
Dog.prototype = new Animal();
Dog.prototype.bark = function () {
  console.log('wang~wang~')
};

var wangCai = new Dog();

// wangCai 可以访问到它的原型 Dog.prototype 上的 bark
wangCai.bark(); // wang~wang~

// Dog.prototype 可以访问到 Animal.prototype 上的 eat
Dog.prototype.eat(); // eating...
```

这是上一章的知识，没什么好奇怪的。但是问题来了，既然`wangCai`可以访问到它的原型`Dog.prototype`上的属性而`Dog.prototype`又可以访问到`Animal.prototype`上的属性，那么`wangCai`可以访问到`Animal.prototype`也就是其「原型的原型」上的属性么，如下图：

```{mermaid}
graph LR
  A[wangCai] -- 可以访问 --> B[Dog.prototype]
  B[Dog.prototype] -- 可以访问 --> C[Animal.prototype]
  A[wangCai] -. ??? .-> C[Animal.prototype]
```

答案是「可以」，也就是说，**实例不仅仅能够访问到其原型上的属性，还能访问到其「原型的原型」上的属性**。

```{mermaid}
graph LR
  A[wangCai] -- 可以访问 --> B[Dog.prototype]
  B[Dog.prototype] -- 可以访问 --> C[Animal.prototype]
  A[wangCai] -- 可以访问 --> C[Animal.prototype]
```

我们可以通过如下代码验证这个观点。

```javascript
// wangCai 访问到了其「原型的原型」也就是 Animal.prototype 上的 eat 属性
wangCai.eat(); // eating...
```

实例`wangCai`从`Dog.prototype`处得到了`bark`属性，从`Animal.prototype`处得到了`eat`，像这种从原型

## 原型链

有「原型的原型」就会有「原型的原型的原型」还会有「原型的原型的原型的原型」以及「原型的原型的原型的原型的原型...」等等等等一大波「原型」汹涌澎湃而来，这就叫**原型链**。

```{mermaid}
graph LR
  a[实例 a] -- 的原型 --> A[A.prototype]
  A -- 的原型 --> B[B.prototype]
  B -- 的原型 --> C[C.prototype]
  C -- 的原型 --> D[...]
```

> 原型链被称为「链」是不是很形象呢。

### 原型继承

当某个实例可以访问到其原型链上某个原型的属性时，我们就说该实例**继承**了这个原型所隶属的构造函数的这个属性。例如上一小节中的实例`wangCai`从`Dog.prototype`处得到了`bark`属性，我们就可以说`wangCai`从`Dog`处继承了`bark`属性，同时`wangCai`还从`Animal.prototype`处得到了`eat`属性，那么我们也可以说`wangCai`从`Animal`继承了`eat`属性，如下图所示：

```{mermaid}
graph LR
  subgraph wangCai
  bark
  eat
  end
  bark -- 继承于 --> B[Dog]
  eat -- 继承于 --> C[Animal]
```

这种从基于原型链的继承方式，叫做**原型继承**。

> 如果按照传统面向对象编程的习惯，我们就可以将`Animal`称为`Dog`的**父类**或**超类**，称`Dog`为`Animal`的**子类**或**派生类**，而`wangCai`则是`Dog`的实例。而构造函数，也可以称为**类**。

### 属性在原型链上的访问规则

### 属性在原型链上的共享规则

## 修复错误的 constructor 属性


未完待续...