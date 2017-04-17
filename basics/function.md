## 函数

**函数**的概念最早来自数学，但是在 JavaScript 中的函数，跟数学中的函数略有不同，它不一定要进行计算，不一定要有参数，也不一定会有结果。简单说来，在 JavaScript 里函数就是一个可以反复使用的代码块，随着学习的深入，你会发觉这么说不准确，目前就暂时姑且用它来做为函数的初步印象好了。

一个简单的函数如下所示，运行下方的代码，使用代码中的函数`goodLuck`自己加油：

```javascript
// 函数的声明
function goodLuck() {
  var i = 3;
  while (i !== 0) {
    console.log('加油！');
    i--;
  }
}

// 函数的调用
// 显示三次'加油！'
goodLuck();
```

## 函数的基本使用方式

### 函数的声明
我们可以使用如下伪代码描述的语法声明一个函数：

```
function 函数名 (参数1, 参数2, 参数3, ...) {
  函数体
}
```

函数的名字就是**函数名**，函数名属于标识符，只能由字母数字下划线组成，并且不能以数字开头，在《变量》一章中有介绍过标识符的规则。声明函数时所用的代码块叫做**函数体**，函数体可以包含任意合法的 JavaScript 代码，这些代码只有在我们调用该函数的时候运行。下边代码是上文提到过的`goodLuck`函数，你能说说哪里是函数名、哪里是函数体么。

```javascript
// 函数的声明
function goodLuck() {
  var i = 3;
  while (i !== 0) {
    console.log('加油！');
    i--;
  }
}
```

### 函数的调用
当我们声明了一个函数了之后，我们就可以**调用**它，执行函数体中的代码，函数调用使用如下伪代码描述的语法：

```
函数名 (参数1, 参数2, 参数3, ...);
```

一个函数在没被调用之前它函数体中的代码是不会运行的，一个函数可以多次被调用，我们每调用一次，它函数体中的代码就执行一次，例如下边代码调用了三次`goodLuck`函数，在控制台输出了九次`'加油!'`：

```javascript
// 函数的声明
function goodLuck() {
  var i = 3;
  while (i !== 0) {
    console.log('加油！');
    i--;
  }
}

// 函数的调用
// 这里调用了三次 goodLuck 函数，每次调用都输出三次「'加油！'」
goodLuck();
goodLuck();
goodLuck();
```

日常编程中，我们就可以事先定义许多的函数，在需要的时候调用它，用到一次调用一次，如此一来，就不用在每次想要使用某个功能的时候都重写一次该功能了。

### 参数传递

在上边的代码中我们看到，当我们需要输出九次`'加油！'`的时候，需要调用三次`goodLuck`，该函数每次调都是输出三次`'加油！'` ，这样不灵活，如果我们希望调用一次`goodLuck`就能输出九次加油，或者说，我们希望调用一次输出一次加油的时候，能不能有调用一次想输出几次`'加油!'`就输出几次的方法？为了解决类似问题我们可以在调用的时候给函数传递参数。JavaScript 中的函数最多能有 255 个参数，最少则一个参数也没有，我们可以根据需要决定函数接受多少参数。下边将对`goodLuck`函数作出修改，使之能够接受参数。

我们在声明`goodLuck`函数的时候，在函数名后边的`()`中告诉 JavaScript 这个函数接受什么参数。

```javascript
// goodLuck 现在接受一个叫做 times 的参数
function goodLuck(times) {
  var i = times; // 将参数的值赋给 i
  while (i !== 0) {
    console.log('加油！');
    i--;
  }
}
```

上边代码中的`times`就是参数的名字，参数名是一种标识符，就像变量名一样，我们可以自行定义它。参数具体的值，我们在声明函数的的时候是不知道的，就像数学函数里 $$f(x) = x + 1$$ 中的 $$x$$ 在我们定义 $$f(x)$$ 的时候是未知数一样。参数的值，是我们在调用函数的时候给它传递的。就像 $$f(5)$$ 中的 $$5$$ 和 $$f(99)$$ 中的 $$99$$。

例如下边的代码就在调用函数`goodLuck`的时候传递了参数`1` `3` `5`，每次调用分别在控制台中输出一次、三次、五次`'加油！'`：

```javascript
// goodLuck 现在接受一个叫做 times 的参数
function goodLuck(times) {
  var i = times; // 将参数的值赋给 i
  while (i !== 0) {
    console.log('加油！');
    i--;
  }
}

// 给 goodLuck 传递了 1 做为参数，
// 此时 goodLuck 函数体中的 times 的值为 1
// 执行效果为输出一次「'加油！'」
goodLuck(1);

// 给 goodLuck 传递了 3 做为参数，
// 此时 goodLuck 函数体中的 times 的值为 3
// 执行效果为输出三次「'加油！'」
goodLuck(3);

// 给 goodLuck 传递了 5 做为参数，
// 此时 goodLuck 函数体中的 times 的值为 5
// 执行效果为输出五次「'加油！'」
goodLuck(5); 
```

在调用函数的时候，参数可以直接传值，也可以使用变量，变量和值还可以混合使用，例如下边的代码中的函数`average`求三个值的平均值，并且将结果输出到控制台上：

```javascript
function average (x1, x2, x3) {
  var result = (x1 + x2 + x3) / 3;
  console.log(result);
}

var a = 5,
    b = 6;

// 使用变量 a b 和数字 7 给函数传递参数
average(a, b, 7); // 6
```
> 小练习，你能说出上面代码中，那些是函数的声明哪些是函数的调用，当函数被调用时，`x1` `x2` `x3`的值分别是什么

同时，参数可以是**任意类型**的数据，例如下边代码中的有三个函数`invert`、`tail`和`reverse`，它们分别使用了对象、数组和字符串做参数。

```javascript
// 接受一个对象作为参数，
// 并在控制台输出一个属性名和属性值倒置的对象
function invert (object) {
  var result = {};
  for (var key in object) {
    result[object[key]] = key;
  }
  console.log(result);
}
invert({name: 'jack', age: 56}); // {jack: 'name', 56: 'age'}
invert({jack: 'name', 56: 'age'}); // {name: 'jack', age: '56'}

// 接受一个数组作为参数，
// 并在控制台输出该数组除了第一个成员以外的其他成员
function tail (array) {
  console.log(array.slice(1));
}
tail([1, 2, 3, 4, 5]); // [2, 3, 4, 5]
tail(['a', 'b', 'c', 'd', 'e']); // ['b', 'c', 'd', 'e']


// 接受一个字符串作为参数，
// 并在控制台输出一个逆序的字符串
function reverse (string) {
  var result = '';
  for (var i = string.length - 1; i >= 0; i--) {
    result = result + string[i];
  }
  console.log(result);
}
reverse('abcde'); // 'edcba'
reverse('12345'); // '54321'
```
> 虽然参数名是可以自行定义的，但是在声明函数的时候，使用英文意思明确的参数名是一个好习惯，方便别人和自己知道你写的函数需要接受怎样的参数。

当函数在调用的时候少传递了某个参数，这个参数在函数体内部的值就是`undefined`，例如下边代码中的`x2` `x3`：

```javascript
function fn(x1, x2, x3) {
  console.log(x1, x2, x3);
}

// fn 要两个参数，单只给它传递了一个
fn(1); // 1 undefined undefined
```
大多数情况下`undefined`不会是我们想要的参数，例如下列代码中的`add`函数是计算三个数的和，由于第三个参数没有传递，出现了两个数与`undefined`相加的情况，结果略显尴尬：

```javascript
function add(x1, x2, x3) {
  console.log(x1 + x2 + x3);
}

// 第三个参数没传递在函数体内计算了
// 1 + 2 + undefined
// 得到了尴尬的结果
add(1, 2); // NaN
```
为了避免此类情况，我们可以通过`if`语句判断参数是否纯在，以便给给参数设置一个缺省值，例如下边代码是改进后的`add`函数，我们判断了它的参数，如果不存在，就设置为`0`：

```javascript
function add(x1, x2, x3) {
  if (x1 === undefined) {
    x1 = 0;
  }
  if (x2 === undefined) {
    x2 = 0;
  }
  if (x3 === undefined) {
    x3 = 0;
  }
  console.log(x1 + x2 + x3);
}

add(1, 2, 3); // 6
add(1, 2); // 3
add(1); // 1
add(); // 0
```

### 函数的返回值

之前的示例函数在调用后都是没有返回值的，当我们需要函数有返回值的时候，可以在函数体里使用`return`语句。下边代码中的两个函数的作用是将两个数相加，一个使用了`return`语句，另外一个没使用：

```javascript
// 没有使用 return
function add1 (x1, x2) {
  x1 + x2;
}
var a = add1(1, 1);
console.log(a); // undefined

// 使用了 return
function add2 (x1, x2) {
  return x1 + x2;
}

var b = add2(1, 1);
console.log(b); // 2
```

通过上边代码我们可以看到，没使用`return`语句的函数，外部得不到`x1 + x2`的结果，而使用了`return`语句的函数可以将结果返回给外部使用。很多时候，我们使用函数是为了对数据进行加工，在这种情况下，我们把加工后的结果返回给外部使用是个很棒的做法。如此一来，函数的职责就会变得明确，它只负责加工数据，不必关心加工后的结果在外部被怎么使用。

上文提到的三个函数`invert`、`tail`和`reverse`就是这种类型的函数，下边的代码修改它们，让它们返回加工数据后的结果：

```javascript
// 接受一个对象作为参数，
// 返回一个属性名和属性值倒置的对象
function invert (object) {
  var result = {};
  for (var key in object) {
    result[object[key]] = key
  }
  return result;
}

// 接受一个数组作为参数，
// 返回数组除了第一个成员意外的其他成员
function tail (array) {
  return array.slice(1);
}

// 接受一个字符串作为参数，
// 返回一个逆序的字符串
function reverse (string) {
  var result = '';
  for (var i = string.length - 1; i>= 0; i--) {
    result = result + string[i];
  }
  return result;
}
```
如此一来函数的外部就可以尽情的使用它们的结果，而不是像原来一样仅仅将结果显示在控制台中，这样函数就会变得更通用，下边代码举例了`tail`的返回值的各种使用方式。

```javascript
// 得到了 tail 函数的结果
var a = tail(['jack', 'tony', 'sam', 'david', 'lily']);

// 可以在控制台中输出它
console.log(a); // ['tony', 'sam', 'david', 'lily']

// 也可以对结果进行修改
a.push('bella');
a.splice(2, 1);

// 还可以将结果再次加工
a = a.slice(1, 3);

// 赋值给别的变量
var b = a;

// 此处省略约一万种操作 a 的方式

// 再次使用 tail 处理别的数组
var c = tail([1, 2, 3, 4, 5]);
// 得到的结果 c 又可以被任意的使用

// 再再次使用 tail 处理其他数组
var d = tail([
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]);
// 得到的结果 d 又可以被任意的使用
/* 等等等等 */
```

一个函数内部可以有多条`retuen`语句，例如下边代码中的函数`isFemale`根据参数`gender`的值判断返回不同的布尔值。

```javascript
// 如果 gender 的值为 'female' 则返回 true 
// 否则返回 false
var isFemale = function (gender) {
  siwtch (gender) {
    case 'female':
      return true;
    default:
      return false;
  }
}
```

### return 语句会让函数直接结束
一个函数内部可以有多条`retuen`语句，但是只有其中一条`retuen`会被执行，因为`return`在执行之后函数会直接退出。，就是当函数执行完该语句之后，函数会直接结束，无论函数体中是否还有其他代码。例如，下面代码只会在控制台输出`1`：

```javascript
function count() {
  console.log(1);
  return 0; // 随便返回一个 0
  console.log(2); // 没被执行，因为函数在 return 后就结束了
  console.log(3); // 同上
}

count(); // 1
```

有的时候，我们仅仅希望函数能够结束，不需要函数返回什么值，我们在使用`return`语句的时候右边就可以什么也没有，例如下边代码对上边的`count`函数做出修改，删掉`return`语句右边的`0`也是合法的：

```javascript
function count() {
  console.log(1);
  return; // return 的右边什么也不跟，是合法的
  console.log(2);
  console.log(3);
}

count(); // 1
```

因为不是所有函数都有必要运行到最后，`return`语句的这种特性可以让我们在合适的时候主动结束掉一个函数，得到或不得到它的返回值，例如，下边的函数`indexOf`，从数组中寻找某个成员的索引，当成员找到函数就可以结束了，没有必要把数组整个找完一遍。

```javascript
// array 是数组
// target 是需要寻找的成员
function indexOf(array, target) {
  for(var i = 0; i < array.length; i++) {
    // 找到了就直接 return 退出函数
    if (array[i] === target) {
      return i;
    }
  }
}

var jackIndex = indexOf(['jack', 'bella', 'lily', 'hank'], 'jack');
console.log(jackIndex); // 0
```

### arguments 变量

之前介绍的所有函数参数的数量都是在函数声明的时候就设定好的，如果我们想要处理参数数量不定的参数的时候，就需要用到函数内部的一个特殊的变量`arguments`，这个变量的内容是这个函数所接受的参数的集合，例如：

```javascript
// 声明的时候只有一个参数
function fn (x) {
  console.log(x, arguments);
}

// 调用的时候给它传递了一堆参数
// arguments 包含了这个函数所接受到的所有参数
fn(111,2,3,4,5); // 111 [111, 2, 3, 4, 5]
```

`arguments`是一个长得很像数组但又不是数组的特殊对象，我们可以通过`[]`操作符取到某个参数的内容：

```javascript
// 通过 [] 操作符取到第一个参数
function fn0 () {
  console.log(arguments[0]);
}
fn0(111,2,3,4,5); // 111

// 通过 [] 操作符取到第三个参数
function fn2 () {
  console.log(arguments[2]);
}
fn2(111,2,3,4,5); // 3
```

同时也可以使用循环语句遍历`arguments`，如此一来，我们就可以通过操作`arguments`来处理参数数量不定的函数了，例如下边代码的`average`函数可以求多个参数的算数平均值：

```javascript
// 不管传入多少个参数，都能求算数平均值
function average () {
  var sum = 0;
  for (var i = 0; i < arguments.length; i++) {
    sum += arguments[i];
  }
  return sum / arguments.length;
}

var a = average(2, 3, 4);
console.log(a); // 3

var b = average(1, 2, 3, 4, 5);
console.log(b); // 3

var c = average(2);
console.log(a); // 2
```

## 函数表达式

实际上函数也是一种数据类型，虽然这理解起来有点别扭，但是仔细想想，不管是函数，还是图片，还是声音，或者是我们学到的字符串、数字、数组等等的东西，在计算机的世界里都是由`0`和`1`组成的。既然都是由`0`和`1`组成的玩意儿，那么 JavaScript 把函数也当作了一种数据类型也就没什么大惊小怪的了，函数表达式，就是返值是函数的一种表达式，它返回的函数就是用函数表达式定义的函数。

### 匿名函数表达式

既然函数表达式的返回值是一个函数，我们可以把这个返回值赋值给变量，这样一来除了之前介绍的的函数声明之外，我们又多了一种创建函数的方式，例如上文的`indexOf`函数也可以这么被创建：

```javascript
// 将函数表达式的返回值赋值给变量 indexOf
var indexOf = function (array, target) {
  for(var i = 0; i < array.length; i++) {
    if (array[i] === target) {
      return i;
    }
  }
}

// 使用的方式和之前一样
var index = indexOf([1, 2, 3, 4, 5],  4);
console.log(index); // 3
```

### 具名函数表达式

函数表达式在多数情况下是匿名的，也就是`function`后边不跟「函数名」的，但是我们也可以使用有名字的函数表达式。例如：

```javascript
// _indexOf 就是函数表达式的名字
var indexOf = function _indexOf (array, target) {
  for(var i = 0; i < array.length; i++) {
    if (array[i] === target) {
      return i;
    }
  }
}

// 使用的方式和之前一样
var index = indexOf([1, 2, 3, 4, 5],  4);
console.log(index); // 3
```
> 虽然看起来多此一举，但是在某些场景中，这是必不可少的。

函数表达式是 JavaScript 中非常有魅力的一部分，我们在讨论高阶函数的时候，就会看到许许多多的函数表达式。

### 函数表达式和函数声明在创建函数时的区别

读者到这里有可能会好奇，都是创建函数，那么使用函数声明和函数表达式的区别在哪呢？函数声明不必先声明后使用，先使用后声明也是可以的，例如下面代码能输出正常值：

```javascript
var jackIndex = indexOf(['jack', 'bella', 'lily', 'hank'], 'jack');
console.log(jackIndex); // 0

function indexOf(array, target) {
  for(var i = 0; i < array.length; i++) {
    // 找到了就直接 return 退出函数
    if (array[i] === target) {
      return i;
    }
  }
}
```
> 尽管如此，先声明后使用是个好习惯。因此，本书往后的代码示例会优先选择使用函数表达式创建一个函数，可以保证函数是先声明后使用的。

而函数表达式就必须先赋值后使用，例如下边代码报错：

```javascript
var jackIndex = indexOf(['jack', 'bella', 'lily', 'hank'], 'jack'); // 报错
console.log(jackIndex);

var indexOf = function (array, target) {
  for(var i = 0; i < array.length; i++) {
    // 找到了就直接 return 退出函数
    if (array[i] === target) {
      return i;
    }
  }
};
```
> 如果是连着上边那个代码框中的代码一块运行的，运行前记得刷新网页。

## 高阶函数
许多其他编程语言中的函数，它们的参数和返回值不能是函数。而 JavaScript 中的函数，不仅可以像其他语言一样使用，还可以使用函数作为参数和返回值。使用函数作为参数或返回值的函数就叫**高阶函数**，他让 JavaScript 变得更加有魅力，在处理许多复杂运算的时候，可以组合各种函数来完成我们所需的任务。

### 函数作为参数和返回值

下边的代码中的`map`函数就是一个典型的高阶函数，它将数组参数`array`中的成员逐个使用函数参数`fn`加工，然后将加工后的结果逐个放入新的数组，参数函数`fn`对数据的处理方式，决定了`map`函数的返回值，非常灵活：

```javascript
// map 函数的第二个参数是一个函数
var map = function (array, fn) {
  var result = [];
  for(var i = 0; i < array.length; i++) {
    var item = array[i]; // item 为数组的当前成员
    var mapped = fn(item); // 调用作为参数的函数 fn，将该成员作为参数传递给它作为它的参数
    result.push(mapped); // result 追加 fn 执行的结果
  }
  return result;
};

// 将每个成员乘以二
var doubleList = map([1, 2, 3, 4, 5, 6], function(item) {
  return item * 2;
});
console.log(doubleList); // [2, 4, 6, 8, 10, 12]

// 将每个成员平方
var squareList = map([1, 2, 3, 4], function (item) {
  return item * item;
});
console.log(squareList); // [1, 4, 9, 16]
```
像上边代码`fn`这种传递给函数参数执行的函数，叫**回调函数**，英文里是 callback。

函数也可以作为返回值，例如，下边代码中的`makeIDGenerator`也是一个高阶函数，它返回了一个每调用一次就递增`1`的函数，实际编程中，我们需要这样的函数来给对象加上递增的`id`，这样`id`不会重复，方便查找和修改：

```javascript
// 函数 makeIDGenerator 的返回值是一个函数
var makeIDGenerator = function () {
  var i = 0;
  return function () {
    return i++;
  }
};

var userIDGenerator = makeIDGenerator();
console.log(userIDGenerator()); // 0
console.log(userIDGenerator()); // 1
console.log(userIDGenerator()); // 2

var messageIDGenerator = makeIDGenerator();
console.log(messageIDGenerator()); // 0
console.log(messageIDGenerator()); // 1
```

## 函数和方法

### 作为对象属性的函数

之前说到函数的调用，可能大家会觉得似曾相识，实际上，我们在进入这章之前，已经有使用过函数了。例如字符串的`slice`数组的`pop` `push`等等。只不过在当时，我们称它们为「方法」。实际上，函数和方法一脉相承。回忆一下对象一章的知识，我们有学到「对象的属性可以是任意类型的数据」，因此对象的属性实际上也能是函数。为了符合面向对象编程的世界观，JavaScript 把这种作为对象属性存在的函数叫做**方法**。

例如下边代码中的对象`user`有一个`sayHiTo`方法：

```javascript
var user = {
  name: 'bella',
  age: 12,
  sayHiTo: function (target) {
    console.log('Hi ~ ' + target);
  }
}

// 方法的调用
user.sayHiTo('jack'); // 'Hi ~ jack'
```

### this 变量初探

当函数作为某个对象的方法的时候，在它的内部会有一个特殊的变量`this`这个变量通常情况下引用着对象本身，例如我们给上边的`user`对象加上一个`selfIntroduction`方法，让它可以进行自我介绍。

```javascript
var user = {
  name: 'bella',
  age: 12,
  sayHiTo: function (target) {
    console.log('Hi ~ ' + target);
  },
  selfIntroduction: function () {
    console.log('My name is ' + this.name); // 通过 this 引用到这个对象的 name 属性
  },
  greetingStart: function (target) {
    this.sayHiTo(target); // 通过 this 引用到这个对象的 sayHiTo 方法
    this.selfIntroduction(); // 通过 this 引用到这个对象的 selfIntroduction 方法
  }
}

user.selfIntroduction(); // 'My name is bella'

user.name = 'Jack Wu';
user.selfIntroduction(); // 'My name is Jack Wu'

user.name = 'Lucy';
user.selfIntroduction(); // 'My name is Lucy'

user.greetingStart('nicky');
// 'Hi ~ nicky'
// 'My name is Lucy'
```
如此一来，当我们在方法内部想使用对象的某些属性的时候，就会变得灵活，许多东西就可以直接通过`this`来访问，而不是写死在代码中。

但是，要吐槽的一点是，之前说的是通常情况下，有时候`this`不会总是乖乖听话的，例如下边代码中，当我们把方法赋值给某个变量后再运行，`this.name`丢了，而`greetingStart`直接报错。

```javascript
var user = {
  name: 'bella',
  age: 12,
  sayHiTo: function (target) {
    console.log('Hi~ ' + target);
  },
  selfIntroduction: function () {
    console.log('My name is ' + this.name); // 通过 this 引用到这个对象的 name 属性
  },
  greetingStart: function (target) {
    this.sayHiTo(target);
    this.selfIntroduction();
  }
}

var selfIntroduction = user.selfIntroduction;
selfIntroduction(); // 'My name is' ，注意 this.name 的值没了
user.selfIntroduction(); // 'My name is bella'，this.name 的值又回来了

var greetingStart = user.greetingStart;
greetingStart('nicky'); // 直接报错
```

不仅是赋值给变量，作为参数传递到其他函数中运行，`this`的值也有可能出乎意料。实际上，`this`变量作为 JavaScript 中最为让人困惑的功能之一，想要彻底弄明白它涉及到其他知识，我们会在往后详细介绍它。现在阶段，如果想要`this`的值正常，我们可以直接使用`属性名.方法名(参数1, 参数2....)`这种格式调用对象的方法。

## 变量的作用域
> 这个小节示例代码中的`undefined`在有些浏览器中会正常显示，在有些浏览器中会直接报错提示「xxxx is not defined」，这取决于浏览器默认运行 JavaScript 中的哪种模式，不管是显示了`undefined`还是报错提示，说的都是该变量访问不到。

我们知道函数体可以包含各种个样的代码，既然如此，函数体内部就能声明变量，那么当函数体外部的变量和函数体内部的变量名字一样的时候该如何是好呢。

```javascript
// 函数体内部有一个变量 i
var makeIDGenerator = function () {
  var i = 0;
  return function () {
    return i++;
  }
};

// 外面也有一个变量 i
var i = 5;

// 当我们调用 makeIDGenerator 的时候，其内部 i 的值是什么呢
var userIDGenerator = makeIDGenerator();
```
### 作用域的基本规则

明白了变量的作用域，就可以很好的解决上面的疑问。变量的作用域可以理解成变量的作用范围，在 JavaScript 中，作用域是以函数为单位的，被称为**函数级作用域**。我们在某个函数内部声明的变量，它的作用范围就在这个函数内部，换句话说，它只能在这个函数内部使用，函数外部，以及其他函数都是访问不到这个变量的，例如下列代码中的`i`变量：

```javascript
var fn = function () {
  var i = 5; // 这里声明了 i 变量
}

// fn 函数的外部访问不到它
console.log(i); // undefined


var func = function () {
  console.log(i);
}

// 其他函数也访问不到它
func(); // undefined
```

而同时，函数外部声明的变量，在所有函数内部都可以访问得到，例如：

```javascript
var i = 5;
var fn = function () {
  console.log(i);
}
var func = function () {
  console.log(i);
}

fn(); // 5
func(); // 5
```

当函数外部声明的变量和内部的变量相同的时候，函数内部使用自己函数体中的变量，而函数外部则使用函数外部的变量，例如：

```javascript
var i = 100;
var fn = function () {
  var i = 5;
  console.log(i);
}

fn(); // 5
console.log(i); // 100
```

> 小练习： 说说出本小节开头时候函数`makeIDGenerator`在调用时其内部的`i`是什么。

### 全局作用域和本地作用域

当一个变量是函数外部被声明的，我们就说该变量存在于**全局作用域**，当变量在某个函数体中被声明的，我们就说这个变量存在于该函数的**本地作用域**，有时候为了方便直接称为「某某函数的作用域」。例如下边的代码标识了全局作用域和`fn` `func`函数的本地作用域：

```javascript
// 从这里一直到代码的结束，是全局作用域
var a = 5,
    b = 8;
    
var fn = function () {
  // 从这里一直到函数结束是函数 fn 的本地作用域
  var fna = 11;
}

var func = function () {
  // 从这里一直到函数结束是函数 func 的本地作用域
  var funca = 22;
}
```

上边代码中全局作用域中有 4 个变量,它们分别是`a` `b` `fn` `func`，而函数`fn`和`func`的本地作用域中各有一个变量，它们是`fna`和`funca`如下图。

```{mermaid}
graph TD
subgraph 全局作用域
  subgraph a

  end
  subgraph b

  end
  subgraph fn
    fna
  end
  subgraph func
    funca
  end
end
```

我们知道，函数能够访问到自己本地作用域中的变量和全局作用域中的变量，不能访问其他函数作用域中的变量。所以上图中函数：

1. `fn`可以访问到变量`a` `b` `fna`但访问不到`funca`
2. `func` 可以访问到变量`a` `b` `funca`但访问不到`fna`。

我们可以用如下代码验证上面的观点。

```javascript
var a = 5,
    b = 8;
    
var fn = function () {
  var fna = 11;
  console.log(a, b, fna, funca);
}

var func = function () {
  var funca = 22;
  console.log(a, b, fna, funca);
}

fn(); // 5 8 11 undefined
func(); // 5 8 undefined 22
```

函数的参数是函数本地作用域中的变量，它在函数被调用的一刻被赋值，同时`arguments`也是这个函数本地作用域中的变量，每个函数它函数体中的`arguments`都是这个函数自己的参数列表，因为这些玩意儿都算是本地作用域中的变量，所以函数外部和其他函数都访问不到它们，例如：

``` javascript
// 找到三个数中最大的数
var max = function (x1, x2, x3) {
  var result = x1;
  if (x2 > result) {
    result = x2;
  }
  
  if (x3 > result) {
    result = x3;
  }
  
  return result;
}

max(3, 4, 6);

// 全局作用域中没有 max 的参数
console.log(x1, x2, x3); // undefined undefined undefined

// 其他函数的本地作用域没有 x1 x2 x3
var fn = function () {
  console.log(x1, x2, x3);
}
fn(); // undefined undefined undefined

// 此时 func 中的 x1, x2, x3 是自己作用域中的，而不是 max 作用域中的
var func = function (x1, x2, x3) {
  console.log(x1, x2, x3);
}
func('a', 'b'); // 'a' 'b' undefined
```

下图标出了上边代码中各个变量的作用范围。

```{mermaid}
graph TD
subgraph 全局作用域
  subgraph max
    arguments
    x1
    x2
    x3
  end

  subgraph fn
    fnarg[arguments]
  end

  subgraph func
    funcarg[arguments]
    funcx1[x1]
    funcx2[x2]
    funcx3[x3]
  end
end
```

### 作用域链

既然函数体中可以是任意合法的代码，那么就可以在函数体中创建函数，在这个被创建的函数的函数体中，又创建函数，接着再创建，再创建，变量的作用域就变的有意思了。JavaScript 管理作用域的规则叫**作用域链**，之前介绍的所有关于作用域的规律都只是作用域链的特殊情况，现在，我们完整的介绍 JavaScript 的作用域规则。

作用域链决定了 JavaScript 在寻找变量时的访问作用域的顺序。当一个函数在执行时用到了某个变量，那么 JavaScript 会首先在这个函数的本地作用域中寻找这个变量，如果找到就直接使用，如果找不到，JavaScript 就到这个函数的父函数的作用域中找，如果找到就使用，如果再找不到，就到这个函数的爷爷函数的作用域中找，以此类推，一直找到全局作用域，找到就使用，找不到就只能是`undefined`了。

```{mermaid}
graph TB
  A{本地作用域}
  A -- 找到 --> return[使用变量]
  A -- 没找到 --> B{父函数作用域}
  B -- 找到 --> return
  B -- 没找到 --> C{爷爷函数作用域}
  C -- 找到 --> return
  C -- 没找到 --> D{...}
  D -- 找到 --> return
  D -- 没找到 --> E{全局作用域}
  E -- 找到 --> return
  E -- 没找到 --> null[undefined]
```

举个例子，有如下函数一堆：

```javascript
// 全局作用域
var g = 20;

var first = function (x) {
  // 第一层作用域
  var a = 1 + x;
  return function second (x) {
    // 第二层作用域
    var b = a + x;
    return function third (x) {
      // 第三层作用域
      var c = b + x;
      console.log(a, b, c, g, x);
    }
  }
}
```

用下图描述了这堆函数作用域的包含关系，从中可以看出每个变量的作用范围。

```{mermaid}
graph TD
subgraph 全局作用域
  g
  subgraph first
    a
    x1[x]
    subgraph second
      b
      x2[x]
      subgraph third
        x3[x]
        c
      end
    end
  end
end
```

当上边代码中`third`函数运行时，在它的内部用到了`a, b, c, g, x`等等一连串的变量（函数的参数算作该函数本地作用域中的变量）。其中`x`和`c`是在`third`本地作用域中找到的，`b`是在`second`的作用域中找到的，`a`是在`first`作用域中找到的，`g`是在全局作用域中找到的，如下图，

```{mermaid}
graph TB
  S[寻找变量 a, b, c, g, x]
  S --> A[third 作用域]
  A -- 找到 x 和 c --> return[使用变量]
  A -- 余下 a, b, g --> B[second 作用域]
  B -- 找到 b --> return
  B -- 余下 a 和 g --> C[first 函数作用域]
  C -- 找到 a --> return
  C -- 余下 g --> D[全局作用域]
  D -- 找到 g --> return
```

下边的代码验证了上边的描述：

```javascript
var g = 20;

var first = function (x) {
  // 第一层作用域
  var a = 1 + x;
  console.log(a, x);
  return function second (x) {
    // 第二层作用域
    var b = a + x;
    console.log(a, b, x);
    return function third (x) {
      // 第三层作用域
      var c = b + x;
      console.log(g, a, b, c, x);
    }
  }
}
// 第一层函数被执行
// a 和 x 在第一层作用域中被找到，值为 2 和 1
var second = first(1); // 2 1

// 第二层函数被执行
// a 在第一层作用域中被找到，值为 2
// b 和 x 则在第二层作用域中被找到，值为 4 和 2
var third = second(2); // 2 4 2

// 第三层函数被执行
// g 在全局作用域中被找到，值为 20
// a 在第一层作用域中被找到，值为 2
// b 在第二层作用域中被找到，值为 4
// c 和 x 在第三层作用域中被找到，值为 7 和 3
third(3); // 20 2 4 7 3
```
> 变量的寻找顺序：
> 1. 第一层函数：第一层作用域 => 全局作用域
> 2. 第二层函数：第二层作用域 => 第一层作用域 => 全局作用域
> 3. 第三层函数：第三层作用域 => 第二层作用域 => 第一层作用域 => 全局作用域

当某个函数被运行时，JavaScript 就这样层层寻找这个函数所使用的变量，这种处理函数作用域的规则，被称为**作用域链**是不是很形象呢。

> 小练习，父函数能访问子函数作用域中的变量么
> 
> ```javascript
> var father = function () {
>   console.log(a);
>   return function son () {
>     var a = 5;
>   }
> }
> 
> father(); // 输出什么呢
> ```

## 立即执行的函数表达式

一开始，先人们在全局作用域中定义和使用变量。随着时代发展，项目的规模越来越大，同一个项目会有多人参与，人人都使用全局作用域，慢慢的，全局作用域就变得拥挤不堪。出现了由于变量名重复而导致的种种 BUG，例如就像之前的一道练习题所示，小明新加入的代码中的变量`x`和小红之前定义的`x`变量名一致，意外导致了小红代码的崩溃。

 ```javascript
 /* 小红之前的代码 */
 var x, y, z, u; // 小红声明了 x
 y = 5;
 x = 3; // x 的值为 3
 z = y % x;
   
   /* 小明新加入的代码 */
 var x, dydx; // 小明又声明了 x
 x = 0; // 小明把 x 的值改为了 0
 dydx = 2 * x + 5;
   
 /* 小红之前的代码 */
 y = 19;
 u = (y + z) / x; // 分母为 0 程序出错
 ```

后来先人们认识到了问题的严重，就发现了「立即执行的函数表达式」这种东西，它如下所示：

```javascript
(function () {
  // 在这里编写自己的代码
})();
```

这种表达式不用刻意去调用，它会立即执行，例如下面代码会直接在命令行中输出`123`，无需额外调用：

```javascript
(function () {
  console.log('123');
})();
```

同时，由于它是一个函数表达式，因此它有着自己的作用域，在它内部定义的变量，在全局作用域中访问不到，不会污染全局作用域。同时，外部也没法修改它本地作用域的变量。所以用它来包裹自己的代码，使用变量名的时候不用害怕会跟其他地方的代码冲突，例如下边代码中用「立即执行的函数表达式」包裹小明新加入的代码，可以排除掉由于变量`x`冲突而导致的 BUG：

 ```javascript
/* 小红之前的代码 */
var x, y, z, u; // 小红声明了 x
y = 5;
x = 3; // x 的值为 3
z = y % x;
   
(function () {
  /* 小明新加入的代码 */
  var x, dydx; // 在「立即执行的函数表达式」内部声明了 x
  x = 0; // 小明把 x 的设置为 0
  dydx = 2 * x + 5;
})();
   
/* 小红之前的代码 */
y = 19;

//「立即执行的函数表达式」 内部的 x 完全没有影响到外部这里的 x ，它还是小红之前设置的 3
console.log(x); // 3
u = (y + z) / x; // 小红代码原来的逻辑得以保留
 ```
> 有了「立即执行的函数表达式」我们就可以将自己的代码和其他代码隔离，降低相互影响的危险，所以在日常开发中，多多使用「立即执行的函数表达式」同时尽量避免直接使用全局作用域是个好习惯。

## 函数的练习

1. 还记得之前写的求最大公约数和分数约分的代码么，将它们包装为函数`gcd`和`reduceFrac`。

    ```
    「你写的代码」
    console.log(gcd(12, 28)); // 4
    console.log(reduceFrac(12, 28)); // [3, 7]
    ```
2. 在不借助数组原生方法的情况下实现一个数组的`slice`函数，这个函数接受三个参数`array` `start`和`end`。

    ```
    「你写的代码」
    var a = slice([1, 2, 3, 4], 1, 4);
    console.log(a); // [2, 3, 4]
    
    ```
3. 将上文提到的`slice`函数改成可变参数版本的，如果第三个参数省略，那么它默认为第一个参数的长度。

    ```
    「你写的代码」  
    var a = slice([1, 2, 3, 4], 1);
    console.log(a); // [2, 3, 4]
    var b = slice([1, 2, 3, 4], 1, 3);
    console.log(b); // [2, 3]   
    ```

4. 写出进行素性测试的函数`isPrime`，编程中如果我们要测试 $$p$$ 是否为素数，可以按照如下说明实现：
 1. 如果 $$p \le 1$$ 为那么它不是素数。
 2. 将 $$p$$ 与$$[2, \sqrt{p}] $$ 区间内的每个整数求模，在此过程中如果存在模为 $$0$$ 的情况那么 $$p$$ 就不是素数，否则 $$p$$ 为素数。

    ```
    「你写的代码」 
	 console.log(isPrime(4)); // false
	 console.log(isPrime(17)); // true
    ```
5. 写一个`max`函数它能从多个参数中找到最大值并返回。

    ```
    「你写的代码」
    max(5, 2, 3, 7, 9); // 9
    max(3, 7); // 7
    max(3, 7, 1, 8); // 8
    ```
6. 写一个`min`函数它能从多个参数中找到最小值并返回。

    ```
    「你写的代码」
    min(5, 2, 3, 7, 9); // 2
    min(3, 7); // 3
    min(3, 7, 1, 8); // 1
    ```
7. 写一个`foreach`函数，它没有返回值，接受两个参数，第一个参数是数组，第二个参数是函数。调用`foreach`函数，能把第一个参数的成员逐个传给第二个参数处理。

    ```
    「你写的代码」
    var result = 0;
    foreach([1, 2, 3, 4, 5], function (item) {
      console.log(item); // 逐个输出 1 2 3 4 5
      result += item;
    });
    console.log(result); // 15
    
    var result = '';
    foreach(['a', 'b', 'c', 'd', 'e'], function (item) {
      console.log(item); // 逐个输出 'a' 'b' 'c' 'd' 'e'
      retult += item;
    });
    console.log(result); // 'abcde';
    ```
8. 写一个`filter`函数，接受两个参数，第一个参数是数组，第二个参数是函数。调用`filter `函数，能把第一个参数的成员逐个传给第二个参数处理，并且将处理结果为`true`的成员传递到一个新数组里并返回新数组。

    ```
    「你写的代码」
    var a = filter([1, 2, 3, 4, 5, 6, 7], function (n) {
      return n % 2 === 0;
    });
    console.log(a); // [2, 4, 6]
    
    var b = filter([1, 2, 3, 4, 5, 6, 7], function (n) {
      return n >= 2 && n <= 5;
    });
    console.log(b); // [2, 3, 4, 5]
    ```

9. 写一个`pick`函数，接受数目不定的参数，第一个参数是一个对象，第二个参数开始是字符串，调用这个函数能从第一个参数对象中选出往后参数字符串标识的属性，并将选出来的属性组成一个新的对象返回。

    ```
    「你写的代码」
    var a = pick({
      name: 'bella',
      gender: 'female',
      age: 30,
      title: 'NodeJS开发'
    }], 'name', 'title');
    console.log(a); // {name: 'bella', title: 'NodeJS开发'}
    
    var b = filter({
      name: 'coconut',
      price: 5,
      type: 'fruit',
      weight: 1,
    }, 'name', 'price', 'weight');
    console.log(b); // {name: 'coconut', price: 5, weight: 1}
    
    var c = pick({
      name: 'bella',
      gender: 'female',
      age: 30,
      title: 'NodeJS开发'
    }], 'name');
    console.log(c); // {name: 'bella'}
    ```

10. 下边代码`#1~#4`各输出什么。

    ```javascript
    var fn = function () {
      console.log(arguments);
      return function () {
        console.log(arguments);
      }
    }
    var a = fn('a', 'b', 'c'); // #1
    a(1, 2, 3); // #2
    
    var func = function (x1, x2, x3) {
      console.log(x1, x2, x3);
      return function (x1, x2, x3) {
        console.log(x1, x2, x3);
      }
    }
    var b = func('a', 'b', 'c'); // #3
    b(1, 2, 3); // #4
    ```

11. 下边代码`#1~#6`各输出什么

    ```javascript
    var x = 5;
    var fn = function (x) {
      return function () {
        console.log(x);
      }
    }
    var a = fn('r');
    a(); // #1
    
    var b = fn();
    b(); // #2
    
    var func = function () {
      return function () {
        console.log(x);
      }
    }
    var c = func('r');
    c('a'); // #3
    c(); // #4
    
    var f = function () {
      return function (x) {
        console.log(x);
      }
    }
    var d = f('r');
    d('a'); // #5
    d(); // #6
    ```
12. 下边代码`#1~#4`各输出什么

    ```javascript
    var item = {
      name: 'coconut',
      price: 5,
      sayPrice() {
        console.log(this.price)
      }
    };
    
    item.sayPrice(); // #1
    
    var sayPrice = item.sayPrice;
    sayPrice(); // #2
    
    var item2 = {
      name: 'banana',
      price: 3,
      getPrice(fn) {
        fn();
      }
    }
    item2.sayPrice = sayPrice;
    item2.sayPrice(); // #3
    
    var fn = function (func) {
      func();
    }
    
    fn(sayPrice); // #4
    ```

12. 下边代码`#1~#4`各输出什么

    ```javascript
    var x = 1;
    var fn = function () {
      var x = 5;
      var a = function () {
        console.log(x);
      }
      a(); // #1
      
      var b = function (x) {
        console.log(x);
      }
      b(3); // #2
      
      var c = function () {
        var x = 9;
        console.log(x);
      }
      b(); // #3
      
      var d = function () {
        return function () {
          console.log(x);
        }
      }
      d()(); // #4
    }
    ```
    > 其中`d()()`是一种简写形式，因为`d()`的返回值是一个函数，在后面再加个`()`就是对`d()`的返回值再调用，就写成了`d()()`。