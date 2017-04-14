## 原型的原型

上一章说道，某个实例的原型就是其构造函数的`prototype`属性，这个属性是一个对象。那既然原型是一个对象，就意味着它也能够通过一个构造函数来创建，如此一来就出现了原型的构造函数，而构造函数作为函数一出生就带有`prototype`属性，那么就出现了「原型的原型」。例如下边代码中，构造函数`Dog`的实例`wangCai`，它的原型（也就是`Dog.prototype`）是通过另外一个构造函数`Animal`创建的，所以`Animal.prototype`就是实例`wangCai`「原型的原型」。

```javascript
var Animal = function () {};

var Dog = function () {};
Dog.prototype = new Animal();

var wangCai = new Dog();
```

下图描述了上边代码中的原型关系：

```{mermaid}
graph LR
  A[wangCai] -- 的原型是 --> B[Dog.prototype]
  B[Dog.prototype] -- 的原型是 --> C[Animal.prototype]
  A[wangCai] -- 的原型的原型是 --> C[Animal.prototype]
```

```flow

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

## 原型链

有「原型的原型」就会有「原型的原型的原型」还会有「原型的原型的原型的原型」以及「原型的原型的原型的原型的原型...」等等等等一大波「原型」汹涌澎湃而来，这就叫**原型链**，如下图：

```{mermaid}
graph LR
  a[实例] --> A[原型]
  A --> B[原型的原型]
  B --> C[原型的原型的原型]
  C --> D[...]
```

### 实例可以访问其原型链上任意原型的属性

下边代码构建了一条原型链。

```javascript
var C = function () {};

var B = function () {};
B.prototype = new C();

var A = function () {};
A.prototype = new B();

var a = new A();
```

上边代码的原型关系如下图描述

```{mermaid}
graph LR
  a[实例 a] -- 的原型 --> A[A.prototype]
  A -- 的原型 --> B[B.prototype]
  B -- 的原型 --> C[C.prototype]
```

通过上一小节我们知道实例不仅可以访问到其原型上的属性，也可以访问到其原型的原型上的属性，但实际上，它可以访问到其原型链上任何一个原型的属性。

```{mermaid}
graph LR
  a[实例 a] -- 可以访问 --> A[A.prototype]
  A -- 可以访问 --> B[B.prototype]
  B -- 可以访问 --> C[C.prototype]
  a -- 可以访问 --> B
  a -- 可以访问 --> C
```

> `a`是构造函数`A`的实例

```{mermaid}
graph LR
  A[A.prototype] -- 可以访问 --> B[B.prototype]
  B -- 可以访问 --> C[C.prototype]
  A -- 可以访问 --> C
```

> `A.prototype` 是构造函数`B`的实例

我们可以通过代码验证上边的观点，如下所示：

```javascript
var C = function () {};
C.prototype.ccc = function () {console.log('该属性在 C.prototype 上');}

var B = function () {};
B.prototype = new C();
B.prototype.bbb = function () {console.log('该属性在 B.prototype 上');}

var A = function () {};
A.prototype = new B();
A.prototype.aaa = function () {console.log('该属性在 A.prototype 上');}

var a = new A();

// 实例 a 访问到了其原型链上各个原型的属性
a.aaa(); // '该属性在 A.prototype 上'
a.bbb(); // '该属性在 B.prototype 上'
a.ccc(); // '该属性在 C.prototype 上'

// A.prototype (构造函数 B 的实例)访问到了其原型链上各个原型的属性
A.prototype.bbb(); // '该属性在 B.prototype 上'
A.prototype.ccc(); // '该属性在 C.prototype 上'
```

之前说道如果某个属性在实例的自身或者其原型上那么`in`操作符返回`true`。实际上，只要属性在实例的自身或是其原型链的任何一个原型上`in`操作符都会返回`true`。

```javascript
console.log('aaa' in a); // true
console.log('bbb' in a); // true
console.log('ccc' in a); // true
```

同样的`for..in`语句中的`in`就是`in`操作符，所以，它也会访问到原型链上的属性。

```javascript
for (var key in a) {
  console.log(key);
  // 'aaa'
  // 'bbb'
  // 'ccc'
}
```

### 属性共享

我们知道构造函数`prototype`上的属性不仅会被它的实例访问到，还会给所有这个构造函数所创建的实例共享，放到原型链上这个规则也是一样的，某个原型的属性会给原型链上游的成员们共享，如下图：

```{mermaid}
graph RL
subgraph ...
  subgraph 原型的原型的原型
    subgraph 原型的原型
      subgraph 原型
        a[实例]
      end
    end
  end
end
```

> 1. 原型的属性由实例分享。
> 2. 「原型的原型」的属性由原型和实例共同分享。
> 3. 「原型的原型的原型」的属性由「原型的原型」、原型、实例共同分享。

我们可以通过下方的代码来验证这个观点。

```javascript
var C = function () {};
C.prototype.getPosition = function () {console.log('该属性在 C.prototype 上');}

var B = function () {};
B.prototype = new C();

var A = function () {};
A.prototype = new B();

var a = new A();

// 原型链上游的各个成员都共享了同一份原型链下游的 getPosition 属性
var result = a.getPosition === C.prototype.getPosition &&
             A.prototype.getPosition === C.prototype.getPosition &&
             B.prototype.getPosition === C.prototype.getPosition;

console.log(result); // true
```

### 属性回溯

我们知道，当原型和实例上的属性重名时，我们通过`实例.属性名`或者`实例['属性名']`的方式访问得到的是实例上的属性。把这种情况放到原型链中，JavaScript 采取了跟作用域链类似的规则，当我们访问一个对象的属性的时候，JavaScript 先从对象自身寻找该属性，如果有这个属性，则返回，没有就从该对象的原型上找，有就返回，再没有就从原型的原型上找，有就返回，再没有就再找，一直找到原型链的尽头，实在没有就返回`null`，如下图所示。

```{mermaid}
graph TB
  A{自身}
  A -- 找到 --> return[返回属性值]
  A -- 没找到 --> B{原型}
  B -- 找到 --> return
  B -- 没找到 --> C{原型的原型}
  C -- 找到 --> return
  C -- 没找到 --> D{原型的原型的原型}
  D -- 找到 --> return
  D -- 没找到 --> E{...}
  E -- 找到 --> return
  E -- 没找到 --> null[null]
```

这也就意味着，原型链上有重名属性的时候，我们会得到离实例最近的原型中的属性值，下面代码将验证这个观点：

```javascript
var C = function () {};
C.prototype.getPosition = function () {console.log('该属性在 C.prototype 上');}

var B = function () {};
B.prototype = new C();
B.prototype.getPosition = function () {console.log('该属性在 B.prototype 上');}

var A = function () {};
A.prototype = new B();

var a = new A();

// C.prototype 是实例 a 原型的原型的原型
// B.prototype 是实例 a 原型的原型
// 它们都有 getPosition 属性
// 因为 B.prototype 离实例 a 比较近，所以我们访问到的是 B.prototype 上的 getPosition 属性
a.getPosition(); // '该属性在 B.prototype 上'
```

从上边代码中我们看到，`B.prototype.getPosition` 阻止了我们通过`a.getPosition`访问到`C.prototype.getPosition`，这种情况被称为**属性屏蔽**。

### 原型继承

当某个实例可以访问到其原型链上某个原型的属性时，我们就说该实例**继承**了这个原型所隶属的构造函数的属性。回到本章一开始的例子`wangCai`从`Dog.prototype`处得到了`bark`属性，我们就可以说`wangCai`从`Dog`处继承了`bark`属性，同时`wangCai`还从`Animal.prototype`处得到了`eat`属性，那么我们也可以说`wangCai`从`Animal`继承了`eat`属性，如下图所示：

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

// wangCai 还可以访问到 Animal.prototype 上的 eat
wangCai.eat(); // eating...
```

```{mermaid}
graph LR
  A[wangCai] -- 访问到了 bark --> B[Dog.prototype]
  B[Dog.prototype] -- 访问到了 eat --> C[Animal.prototype]
  A[wangCai] -- 访问到了 eat --> C[Animal.prototype]
```

的继承关系就可以图示为

```{mermaid}
graph LR
  subgraph wangCai
    bark
    eat
  end
  bark -- 继承于 --> B[Dog]
  eat -- 继承于 --> C[Animal]
```

```{mermaid}
graph LR
  subgraph Dog.prototype
    eat
  end
  eat -- 继承于 --> C[Animal]
```

这种基于原型链的继承方式，叫做**原型继承**，是 JavaScript 实现面向对象编程中继承思想的方法。

> 如果按照传统面向对象编程的习惯，也有不少人将 JavaScript 中的构造函数直接称为**类**。按照这种习惯称呼，`Animal`可以称为`Dog`的**父类**，`Dog`称为`Animal`的**子类**，而`wangCai`则是`Dog`的实例。

## 修复错误的 constructor 属性

通过之前所学的知识，我们已经能够使用`JavaScript`来实现各种面向对象的思想，但是还有一个小瑕疵，那就是函数`prototype`属性上自带的`constructor`属性丢失了。在上一章的时候我们说道，每个函数一出生就有`prototype`属性，而`prototype`属性一出生就有`constructor`属性，这个属性的值是函数自身。

```javascript
// 创建一个函数
var A = function () {};

// 该函数一出生就有 prototype 属性
console.log(A.prototype); // {constructor: A}

// prototype 对象一出生就带有 constructor 属性
// 该属性的值是 A 函数本身
console.log(A.prototype.constructor === A); // true
```

当我们将该函数作为构造函数创建实例时，实例也能访问到`constructor`。

```javascript
var a = new A();
console.log(a.constructor === A); // true
```

当原型链只有实例和原型时一切都很顺理成章，但是如果原型链的成员多了起来，就会有问题了，因为，有的构造函数里的`prototype`已经不是默认的带有`constructor`属性的那个对象了，而是其他构造函数创建的，这也就意味着，它原来`prototype`对象里的`constructor`丢了。

```javascript
var C = function () {};

var B = function () {};
B.prototype = new C(); // B.prototype 已经不是默认的那个对象了，而是 new C() 创建的

var A = function () {};
A.prototype = new B(); // A.prototype 已经不是默认的那个对象了，而是 new B() 创建的

var a = new A();
```

因此当我们企图通过`constructor`属性来寻找某个实例的来源的时候会出现问题。

```javascript
console.log(a.constructor === A); // false
```

所以，为了避免留下隐患我们最好手动的修复这个问题，在创建原型链的时候手动的给`prototype`属性附上相应的值即可。

```javascript
var C = function () {};

var B = function () {};
B.prototype = new C();
B.prototype.constructor = B;

var A = function () {};
A.prototype = new B();
A.prototype.constructor = A;

var a = new A();

console.log(a.constructor === A); // true
```
