## 定时器

有时候我们需要过一段时间再运行代码，或者是每隔一段时间运行一次代码，此时就可以使用 JavaScript 提供的定时器。JavaScript 提供了两种定时器`setTimeout`和`setInterval`。 `setTimeout`可以让代码过段时间再运行，而`setInterval`可以让代码每隔一段时间运行一次。

## setTimeout

### 使用 setTimeout 创建延时任务

使用`setTimeout`可以让某段代码过段时间再运行，这在某些场景中特别有用。`setTimeout`是一个函数，它的第一个参数是过段时间要执行的函数，第二个参数是延迟时长，以毫秒为单位，例如，下边代码执行后会过三秒在控制台里输出`'你好'`：

```javascript
setTimeout(function callback () {
  console.log('你好');
}, 3000);
```

如果我们想给`setTimeout`函数中的`callback`传递参数，可以使用`setTimeout`的第二个参数之后的参数。例如下边代码将过三秒在控制台输出`'你好，春天'`：

```javascript
setTimeout(function callback (salutation, name) {
  console.log(salutation + ',' + name);
}, 3000, '你好', '春天');
```
> 这种向`setTimeout`第一个参数函数传递参数的方法在 IE9 及以下浏览器中无效。

### 使用 clearTimeout 清除延时任务

既然`setTimeout`是一个函数，那么它就会有返回值，它的返回值是一个数字ID，而`clearTimeout`可以接受这个数字ID并清除掉这个ID所代表的定时器，如此一来，这个定时器中的逻辑就不会被执行了，例如下边代码中的`setTimeout`被清除了，它什么也不输出：

```javascript
var timerID = setTimeout(function (salutation, name) {
  console.log(salutation + ',' + name);
}, 3000, '你好', '春天');

// 前边的 setTimeout 还没被执行就被清除了
// 所以这段代码什么也不输出
clearTimeout(timerID);
```

## setInterval

### 使用 setInterval 创建周期任务

`setInterval`可以让代码每隔一段时间运行一次，和`setTimeout`类似，它的第一个参数是个函数，这个函数每隔段时间就会执行，第二个参数是周期时长，以毫秒为单位，例如下边代码每隔一秒钟在控制台输出`1`：

```javascript
setInterval(function () {
  console.log(1);
}, 1000);
```

我们也可以使用和`setTimeout`一样的方式给`setInterval`的第一个参数传参，例如下边代码每隔三秒在控制台输出一次`'你好，春天'`：

```javascript
setInterval(function (salutation, name) {
  console.log(salutation + ',' + name);
}, 3000, '你好', '春天');
```
> 这种向`setInterval`第一个参数函数传递参数的方法在 IE9 及以下浏览器中无效。

### 使用 clearInterval 清除周期任务

如果你执行了上边`setInterval`的代码，你会发觉除非刷新页面，否则它完全停不下来，这个时候我们就需要`clearInterval`来清除`setInterval`创建的周期任务，`setInterval`的返回值是个数字ID，将这个ID传递给`clearInterval`就可以清除该ID所代表的周期任务，例如下边是一个十秒倒计时，

```javascript
var countDown = 10;
var timerID = setInterval(function () {
  console.log(countDown);
  countDown--;
  if (countDown === 0) {
    clearInterval(timerID); // 清除周期任务，计时停止
  }
}, 1000);
```
> 因为`setInterval`会马上返回值，而它第一个参数中的代码不会立即执行（要到时间了才执行），所以第一个参数中能访问`timeID`没什么奇怪的。

## 同步和异步

在这章之前，我们接触到的所有代码都是同步执行的，也就是说，当某些代码被执行的时候，它都是从上往下一行一行的执行的。但是同步执行放在延时任务和周期任务里就行不通，因为 JavaScript 不可能在时间没到之前就一直等着不执行的别的任务。所以就有了异步执行的过程，异步执行在 JavaScript 中是个很重要的概念，因为 JavaScript 的世界里有许多需要等待的任务，比如请求某个网页需要等请求到了才执行相关逻辑，网页上某个按钮的逻辑，要等用户点击了这个按钮才运行等等。

所谓异步执行，就是某段代码它不会马上执行，而是在某个事件被触发的时候才执行它。`setTimeout`和`setInterval`就是异步执行的例子，例如下边代码会先输出`2`再输出`1`：

```javascript
setTimeout(function callback () {
  console.log(1)
}, 1000);

console.log(2);
```

上边的`setTimeout`相当于告诉 JavaScript ，让它注意一个「timeout」事件，叮嘱它当「timeout」事件来的时候调用`callback`函数，然后一秒钟后这个「timeout」事件被触发，`callback`被执行。

而「timeout」事件不一定是在整整一秒后被触发，并导致`callback`被执行的，事件的触发通常情况下会慢一些，这跟 JavaScript 内部的运行细节有关，我们会在往后详细的说明这个知识。但不管怎样 JavaScript 一定会先忙完手头上的事情，才处理这些事件，例如就算延时被改为了`0`还是会先输出`2`再输出`1`：

```javascript
setTimeout(function callback () {
  console.log(1)
}, 0);

console.log(2); // #1
```

上边的`setTimeout`相当于告诉 JavaScript ，让它注意一个「timeout」事件，叮嘱它当「timeout」事件来的时候调用`callback`函数，然后 JavaScript 去执行`#1`去了，直到它忙完手头上的事情（通常来说时间非常短），「timeout」事件被触发，`callback`被执行。

## 定时器练习