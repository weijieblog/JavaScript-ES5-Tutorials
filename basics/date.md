## 计算机世界中的时间

在计算机的世界里，表示时间有各种各样的方式，它们并不一定适合人类阅读，例如下边列出了时间`2004-05-03 17:30:08`的一些表示方式。

1. 2004-05-03T17:30:08+08:00
2. 1083576608000
3. Mon May 03 2004 17:30:08 GMT+0800 (CST)
4. 2004-05-03 17:30:08

在现实开发的时候，我们往往要给用户展现适合人类阅读的时间。此时我们就需要 JavaScript 提供的`Date`。

## 创建 Date 对象
> 本小节中使用`console.log`输出「Date 对象」的时候，不同时区不同浏览器输出的内容可能不一样，但表示的是相同的时间。
> 如果想获得和本书一样的输出结果，可以使用 Chrome 浏览器

`Date`是一个函数，通过`new Date(...)`的形式调用，可以得到一个「Date 对象」方便我们处理时间，例如下列代码中我们得到了一个「Date 对象」`time`，它表示了当前的时间。

```javascript
var time = new Date();
console.log(time); // Mon Mar 20 2017 01:43:55 GMT+0800 (CST)
```
> 注意上边代码中的`time`才是`Date`对象，而`new Date()`中的`Date`并不是它是个函数。
> 上边输出的时间是我写作时的时间，不同时间调用结果不一样。


如果我们希望得到的不是当前时间，而是某个时间，就可以给`new Date(...)`传入参数，例如下列代码将`1083576608000`(2004-05-03 17:30:08)作为参数传入。

```javascript
var time = new Date(1083576608000); // 注意这里的参数是数字而不是字符串
console.log(time); // Mon May 03 2004 17:30:08 GMT+0800 (CST)
```


`new Date(...)`可以所有通用的表示时间的方式，例如下边代码中，将`2004-05-03 17:30:08`的各种表示方式传入`new Date(...)`，都能得到正确的「Date 对象」：

```javascript
// 下面各行均输出 Mon May 03 2004 17:30:08 GMT+0800 (CST)
console.log(new Date('2004-05-03T17:30:08+08:00'));
console.log(new Date(1083576608000));
console.log(new Date('Mon May 03 2004 17:30:08 GMT+0800 (CST)'));
console.log(new Date('2004-05-03 17:30:08'));
```

如果在调用`Date`的时候省略了`new`操作符，得到的是一个表示时间的字符串，而不是时间对象，这通常不是我们想要的。

```javascript
var obj = new Date('2004-05-03T17:30:08+08:00');
console.log(typeof obj); // object

var str = Date('2004-05-03T17:30:08+08:00');
console.log(typeof str); // string
```
> `typeof` 可以查看某个值的类型。它通常不安全，往后会讲述安全的判断类型的方式。

## 操作 Date 对象

### getFullYears

### getMonth

### getDate

### getHours

### getMinutes

### getSeconds


## Date 中的实用方法

### Date.now()

### Date.parse()