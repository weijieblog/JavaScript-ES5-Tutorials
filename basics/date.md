## 计算机世界中的时间

在计算机的世界里，表示时间有各种各样的方式。人类有人类表达时间的方式，计算机有计算机表达时间的方式，将计算机表达时间的方式在屏幕上显示出来的时候它们并不一定适合人类阅读，例如下边列出了时间`2004年5月3日 17时30分8秒`在计算机世界里的一些表示方式。

1. 2004-05-03T17:30:08+08:00
2. 1083576608000
3. Mon May 03 2004 17:30:08 GMT+0800 (CST)
4. 2004-05-03 17:30:08

在现实开发的时候，我们往往要给用户展现适合人类阅读的时间表达方式，或是处理一些跟时间相关的逻辑。此时我们就需要 JavaScript 提供的`Date`。

## 创建 Date 对象
> 本小节中使用`console.log`输出「Date 对象」的时候，不同时区不同浏览器输出的内容可能不一样，但表示的是相同的时间。
> 如果想获得和本书一样的输出结果，可以使用 Chrome 浏览器

`Date`是一个函数，通过`new Date(...)`的形式调用，可以得到一个「Date 对象」，这种对象一出生就自带各种可以方便我们处理时间的方法，它是一种**内置对象**。之前我们已经学过如何定义自己的对象，而内置对象区别于我们自己的定义的对象，它是 JavaScript 事先就给我们定义好的对象，这种对象往往带有许多实用的方法和属性，下列代码我们得到了一个「Date 对象」`time`，它表示了当前的时间。

```javascript
var time = new Date(); // 没有参数
console.log(time); // Mon Mar 20 2017 01:43:55 GMT+0800 (CST)
```
> 注意上边代码中的`time`才是`Date`对象，而`new Date()`中的`Date`并不是，它是个函数。
> 上边输出的时间是我写作时的时间，不同时间调用结果不一样。


如果我们希望得到的不是表示当前时间的「Date 对象」，而是具体到某个时间的时候，就可以给`new Date(...)`传入参数，例如下列代码将`1083576608000`(在中国人的眼里，这个时间是：2004年5月3日 17时30分8秒)作为参数传入，得到一个表示`2004年5月3日 17时30分8秒`的「Date 对象」。

```javascript
var time = new Date(1083576608000); // 有参数，得到的是参数表示的时间
console.log(time); // Mon May 03 2004 17:30:08 GMT+0800 (CST)
```


`new Date(...)`可以传入各种计算机常用的时间表达方式，例如下边代码中，将`2004年5月3日 17时30分8秒`的各种表示方式传入`new Date(...)`，都能得到正确的「Date 对象」，但如果传入的参数错误，会得到一个非法的「Date 对象」，这个「Date 对象」不表示任何的时间：

```javascript
// 下面各行均输出 Mon May 03 2004 17:30:08 GMT+0800 (CST)
console.log(new Date('2004-05-03T17:30:08+08:00'));
console.log(new Date(1083576608000));
console.log(new Date('Mon May 03 2004 17:30:08 GMT+0800 (CST)'));
console.log(new Date('2004-05-03 17:30:08'));

// 传入错误的参数
console.log(new Date('中文')); // Invalid Date
```

如果在调用`Date`的时候省略了`new`操作符，得到的是一个计算机表示时间的字符串，而不是「Date 对象」。

```javascript
var obj = new Date('2004-05-03T17:30:08+08:00');
console.log(typeof obj); // object

var str = Date('2004-05-03T17:30:08+08:00');
console.log(typeof str); // string
```
> `typeof` 可以查看某个值的类型。它通常不安全，往后会讲述安全的判断类型的方式。


关于`new`的功能会在本书往后的章节中介绍。

## 使用 Date 对象处理时间

在有了「Date 对象」之后我们就可以使用它提供的方法来处理一些时间相关的内容了，这个小节以将不适合人类阅读的时间表达方式`1083576608000`，转变为适合中国人阅读的表达方式`2004年5月3日 17时30分8秒`为线索，逐个介绍「Date 对象」自带的常用方法。

首先，我们的得到一个叫做`time`的「Date 对象」，`result`为转变后的结果。

```javascript
var time = new Date(1083576608000);
var result;
```

### getFullYear

「Date 对象」的`getFullYear`方法可以得到这个「Date 对象」所代表的时间的四位数年份，以数字的形式返回，这个方法没有参数。

```javascript
result = time.getFullYear();
console.log(result); // 2004
```

### getMonth

「Date 对象」的`getMonth`方法可以得到这个「Date 对象」所代表的时间的月份，以数字的形式返回取值范围是`0~11`，这个方法没有参数。

```javascript
// getMonth 方法得到的月份是从 0 开始的，
// 而我们日常生活中的月份是从 1 开始的所以这里要 「 + 1 」
var month = time.getMonth() + 1;

result = result + '年' + month + '月';
console.log(result); // '2004年5月'
```

### getDate

「Date 对象」的`getDate`方法可以得到这个「Date 对象」所代表的时间的在月中的一天，以数字的形式返回，取值范围是`1～31`，这个方法没有参数。

```javascript
var date = time.getDate();

result = result + date + '日' + ' ';
console.log(result); // '2004年5月3日 '
```

### getHours

「Date 对象」的`getHours`方法可以得到这个「Date 对象」的小时，以数字的形式返回，取值范围是`0～23`，这个方法没有参数。

```javascript
var hours = time.getHours();

result = result + hours + '时';
console.log(result); // '2004年5月3日 17时'
```

### getMinutes

「Date 对象」的`getMinutes`方法可以得到这个「Date 对象」的分钟数，以数字的形式返回，取值范围是`0～59`，这个方法没有参数。

```javascript
var minutes = time.getMinutes();

result = result + minutes + '分';
console.log(result); // '2004年5月3日 17时30分'
```

### getSeconds

「Date 对象」的`getSeconds`方法可以得到这个「Date 对象」的秒数，以数字的形式返回，取值范围是`0～59`，这个方法没有参数。

```javascript
var seconds = time.getSeconds();

result = result + seconds + '秒';
console.log(result); // '2004年5月3日 17时30分8秒'
```

至此，我们已经完成了时间显示方式的转换。将时间`1083576608000`，转变为适合中国人阅读的表达方式`2004年5月3日 17时30分8秒`。

### 格式化时间函数

将计算机表达时间的格式转化为符合人类阅读习惯的格式是一个很常用的功能，因此我们可以写一个函数来处理这个过程，如此一来，每次想要转换时间格式的时候，直接调用这个方法就好。

```javascript
var dateFormat = function (date) {
  var time = new Date(date),
      result;
  
  result = time.getFullYear();
  
  var month = time.getMonth() + 1;
  result = result + '年' + month + '月';
  
  var date = time.getDate();
  result = result + date + '日' + ' ';
  
  var hours = time.getHours();
  result = result + hours + '时';
  
  var minutes = time.getMinutes();
  result = result + minutes + '分';
  
  var seconds = time.getSeconds();
  result = result + seconds + '秒';
  
  return result;
}

dateFormat(Date()); // 2017年3月21日 3时23分26秒 #1
dateFormat(1083576608000); // 2004年5月3日 17时30分8秒
dateFormat('错误的时间表达方式'); // NaN年NaN月NaN日 NaN时NaN分NaN秒 #2
```
> `#1`处没有使用`new`操作符，`Date()`返回的是计算机表达当前时间的字符串
> `#2`处传入了一个不能识别的时间，得到了一个非法的「Date 对象」，该对象自带的各种获取年月日的方法均会返回`NaN`

## Date 中的实用方法

### Date.now()

### Date.parse()