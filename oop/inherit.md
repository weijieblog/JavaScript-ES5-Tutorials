## 原型的构造函数

上一章说道，某个实例的原型就是其构造函数的`prototype`属性，这个属性是一个对象，叫做该实例的原型。那既然原型也是一个对象，也就意味着它能够通过构造函数来创建，事情就变得有意思了呢，例如下边代码中，构造函数`Female`的实例`annie`，它的原型（也就是`Female.prototype`）是通过另外一个构造函数`Person`创建的。

```javascript
var Person = function () {};

var Female = function () {};
Female.prototype = new Person();

var annie = new Female();

console.log(annie instanceof Female); // true
console.log(Female.prototype instanceof Person); // true
```

未完待续...