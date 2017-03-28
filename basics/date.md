## 计算机世界中的时间

人类有人类表达时间的格式，计算机有计算机表达时间的格式，将计算机表达时间的格式在屏幕上显示出来的时候它们并不一定适合人类阅读，例如下边列出了时间「2004年5月3日 17时30分8秒」在计算机世界里的一些格式。

1. 2004-05-03T17:30:08+08:00
2. 1083576608000
3. Mon May 03 2004 17:30:08 GMT+0800 (CST)
4. 2004-05-03 17:30:08

在现实开发的时候，我们往往要给用户展现适合人类阅读的时间格式，或是处理一些跟时间相关的逻辑。此时我们就需要 JavaScript 提供的`Date`函数。

## 创建 Date 对象
> 本小节中使用`console.log`输出「Date 对象」的时候，不同时区不同浏览器输出的内容可能不一样，但表示的是相同的时间。
> 如果想获得和本书一样的输出结果，可以使用 Chrome 浏览器，并将时区设置为东八区。

`Date`是一个函数，通过`new Date(参数)`的形式调用，可以得到一个「Date 对象」，这种对象一出生就自带各种可以方便我们处理时间的方法，它是一种**内置对象**。内置对象区别于我们自己的定义的对象，它是 JavaScript 事先给我们定义好的对象，这种对象一出生就带有许多 JavaScript 提供给我们的方法和属性，方便我们处理某些特定问题。下列代码中，我们通过`new Date()`得到一个「Date 对象」`time`，它表示了当前的时间。

```javascript
var time = new Date(); // 没有参数
console.log(time); // Mon Mar 20 2017 01:43:55 GMT+0800 (CST)
```
> 注意上边代码中的`time`才是`Date`对象，而`new Date()`中的`Date`并不是，它是个函数。
> 上边输出的时间是我写作时的时间，不同时间调用结果不一样。


`new Date()`在不传入任何参数时得到的是表示当前时间的「Date 对象」，当我们想要具体到某个时间的的「Date 对象」的时候，就可以给`new Date()`传入参数，例如下列代码将`1083576608000`(计算机表示时间的格式之一，在人类眼里这个时间是：「2004年5月3日 17时30分8秒」)作为参数传入，得到一个指定时间的「Date 对象」。

```javascript
var time = new Date(1083576608000); // 有参数，得到的是参数表示的时间
console.log(time); // Mon May 03 2004 17:30:08 GMT+0800 (CST)
```


`new Date(...)`可以传入各种计算机常用的表示时间的格式，例如下边代码中，将「2004年5月3日 17时30分8秒」在计算机世界的各种表示方式传入`new Date(...)`，都能得到正确的「Date 对象」，但如果传入的参数 JavaScript 不能识别，会得到一个非法的「Date 对象」，这个「Date 对象」不表示任何的时间：

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

## 时间差
两个「Date 对象」之间可以使用`-`（减法操作符）相减，所得的结果是两个「Date 对象」之间的时间差，以毫秒的形式返回。

```javascript
var a = new Date();

setTimeout(function () {
  var b = new Date();
  console.log(b - a); // 1002
}, 1000);
```
> 为什么不是整整 1000 毫秒？因为`setTimeout`的回调函数通常会慢一些。

因此我们就可以通过「Date 对象」可以相减的特性来简单的评估某个程序的耗时。

```javascript
var i = 0;
var a = new Date();
while(i < 10000000) {
  i++;
}

var b = new Date();
console.log(b - a); // 26
```

也可以知道某个时间距离现在过去了多久，例如下面代码就是计算现在距离「2004年5月3日 17时30分8秒」过去了多少天。

```javascript
var DAY_IN_MILLISECOND = 1000 * 60 * 60 * 24; // 一天的毫秒数

var a = new Date(); // 现在
var b = new Date(1083576608000); // 2004年5月3日 17时30分8秒

console.log((a - b) / DAY_IN_MILLISECOND); // 4705.407994398148
```

## 使用 Date 对象处理时间

在有了「Date 对象」之后我们就可以使用它提供的方法来处理一些时间相关的内容了，这个小节以将不适合人类阅读的时间格式`1083576608000`，转变为适合中国人阅读的格式`'2004年5月3日 17时30分8秒'`为线索，逐个介绍「Date 对象」自带的常用方法。

首先，我们的得到一个叫做`time`的「Date 对象」，`result`变量用来存放转变的结果。

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
> 别忘了当用`+`拼接数字和字符串的时候，最后得到的结果是字符串，详见《字符串》一章。

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

至此，我们已经完成了时间显示方式的转换。将时间`1083576608000`，转变为适合中国人阅读的表达方式`'2004年5月3日 17时30分8秒'`。

### 格式化时间函数

将计算机表达时间的格式转化为符合人类阅读习惯的格式是一个很常用的功能，因此我们可以写一个函数来处理这个过程，如此一来，每次想要转换时间格式的时候，直接调用这个函数就好。

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

dateFormat(Date()); // '2017年3月22日 13时23分26秒' #1
dateFormat(1083576608000); // '2004年5月3日 17时30分8秒'
dateFormat('错误的时间表达方式'); // 'NaN年NaN月NaN日 NaN时NaN分NaN秒' #2
```
> `#1`处没有使用`new`操作符，`Date()`返回的是计算机表达当前时间的字符串，不同时候运行的得到的结果不一样。
> 
> `#2`处传入了一个不能识别的时间，得到了一个非法的「Date 对象」，该对象自带的各种获取年月日的方法均会返回`NaN`。

## Date 中的实用方法

`Date` 虽然是个函数，但是我们还是可以通过`.`或者`[]`访问其中的方法。其中`now`和`parse`是它自带的方法中最常用的两个。

### Date.now

`Date`的`now`方法可以让我们获取从「1970-01-01 00:00:00」至今的毫秒数，以数字形式返回。

```javascript
var now = Date.now();
console.log(now); // 1490100142549
console.log(dateFormat(now)); // '2017年3月21日 20时42分22秒'
```

「1970-01-01 00:00:00」至今的毫秒数是计算机表达时间的最通用的格式之一，这里的「1970-01-01 00:00:00」是格林威治时间，如果换算为中国大陆所在的东八区当地时间则是「1970-01-01 08:00:00」。

```javascript
dateFormat(0); // '1970年1月1日 8时0分0秒'
```

### Date.parse

`Date`的`parse`方法可以将各种计算机用来描述时间的格式统一转化为从「1970-01-01 00:00:00」至今的毫秒数，以数字形式返回，例如：

```javascript
// 下面各行均输出 1083576608000
console.log(Date.parse('2004-05-03T17:30:08+08:00'));
console.log(Date.parse('Mon May 03 2004 17:30:08 GMT+0800 (CST)'));
console.log(Date.parse('2004-05-03 17:30:08'));

console.log(dateFormat(1083576608000)); // 2004年5月3日 17时30分8秒
```

`Date.parse` 方法的参数不能是「1970-01-01 00:00:00」至今的毫秒数本身，例如：

```javascript
console.log(Date.parse(1083576608000)); // NaN
```

实际上当我们在使用`new Date(...)`的时候，它的内部就有调用这个方法，将各种计算机使用的时间格式统一为「1970-01-01 00:00:00」至今的毫秒数再做进一步处理。

## Date 对象练习

1. 将时间`1490124286573`转化为「YYYY年M月D日 H时M分S秒」的形式。

    ```
    var a = new Date(1490124286573);
    var result;
    「你写的代码」
    console.log(result); // '2017年3月22日 3时24分46秒'
    ```

2. 写一个函数，将各种格式的计算机时间转化为「YYYY-M-D H:M:S」的形式。

    ```
    var timeFormat = function (time) {
     「你写的代码」    
    };
    timeFormat(1490124286573); // '2017-3-22 3:24:46'
    timeFormat('Mon May 03 2004 17:30:08 GMT+0800 (CST)'); // '2004-5-3 17:30:08'
    ```
2. 写一个函数，将各种格式的计算机时间转化为「YYYY/M/D H:M:S」的形式。

    ```
    var timeFormat = function (time) {
     「你写的代码」    
    };
    timeFormat(1490124286573); // '2017/3/22 3:24:46'
    timeFormat('Mon May 03 2004 17:30:08 GMT+0800 (CST)'); // '2004/5/3 17:30:08'
    ```

3. 写一个函数，判断某个「Date 对象」是否合法。

    ```
    var isValidDate = function (date) {
     「你写的代码」    
    };
    isValidDate(new Date(1490124286573)); // true
    isValidDate(new Date('哈哈哈哈哈')); // false
    ```

4. 写代码评估函数`a`和函数`b`各自在参数为`1000000`时执行的耗时。

    ```
    var a = function (times) {
      var result = [];
      for (var i = 0; i <= times; i++) {
        result.push({});
      }
      return result;
    }
    
    var b = function (times) {
      var result = [];
      for (var i = 0; i <= times; i++) {
        result[i] = {};
      }
      return result;
    }
    ```
5. 写代码计算时间`1490124286573`距离现在过去了多少小时。
6. 写代码计算时间`1490186974431`和`1490124286573`相差多少小时。
7. 写一个函数，将各种计算机时间格式转化为「YYYY-MM-DD HH:MM:SS」的形式。

    ```
    var timeFormat = function (time) {
     「你写的代码」    
    };
    timeFormat(1490124286573); // '2017-03-22 03:24:46'
    timeFormat('Mon May 03 2004 17:30:08 GMT+0800 (CST)'); // '2004-05-03 17:30:08'
    ```
    > 注意：当月份、日期、时、分、秒为个位数时，在它们前面的数字`0`