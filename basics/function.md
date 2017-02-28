## 函数

**函数**的概念最早来自数学，但是在 JavaScript 中，它跟数学中的函数概念略有不同，它不一定要进行计算，不一定要有参数，也不一定会有结果。简单说来，在 JavaScript 里函数就是一个可以反复使用的代码块，随着学习的深入，你会发觉这么说不准确，目前就暂时姑且用它来做为函数的初步印象好了。

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

一个函数在没被调用之前它函数体中的代码是不会运行的，一个函数可以多次被调用，我们每调用一次，它函数体中的代码就被执行一次，例如下边代码调用了三次`goodLuck`函数，在控制台输出了九次`'加油!'`：

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

在日常编程中，我们就可以事先定义许多的函数，在需要的时候调用它，用到一次调用一次，如此一来，就不用在每次想要使用某个功能的时候都重写一次该功能了。

### 参数传递

在上边的代码中我们看到，当我们需要输出九次`'加油！'`的时候，需要调用三次`goodLuck`，该函数每次调都是输出三次`'加油！'` ，这样不灵活，如果我们希望调用一次`goodLuck`就能输出九次加油，或者说，我们希望调用一次输出一次加油的时候，能不能有调用一次想输出几次`'加油!'`就输出几次的方法？为了解决类似问题我们可以在调用的时候给函数传递参数。JavaScript 中的函数最多能有 255 个参数，最少则一个参数也没有，我们可以根据需要决定函数接受多少参数。下边将对`goodLuck`函数作出修改，使之能够接受参数。

首先，我们在声明`goodLuck`函数的时候，在函数名后边的`()`中告诉 JavaScript 这个函数接受什么参数。

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

### return 语句会让函数直接结束
`return`语句有一个特性，就是当函数执行完它之后，函数会直接结束，无论函数体中是否还有其他代码。例如，下面代码只会在控制台输出`1`：

```javascript
function count() {
  console.log(1);
  return 0; // 随便返回一个 0
  console.log(2); // 没被执行，因为函数在 return 后就结束了
  console.log(3); // 同上
}

count(); // 1
```

有的时候，我们仅仅希望函数能够结束，不需要函数返回什么值，我们在使用`return`语句的时候右边可以什么也没有，例如上边的`count`函数可以做出如下修改：

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
> 虽然看起来多此一举，但是在某些场景中，是能够派上用场的的。

函数表达式是 JavaScript 中非常有魅力的一部分，我们在讨论高阶函数的时候，会说函数表达式的使用场景，匿名的和具名的函数表达式的区别。

### 函数表达式和函数声明在创建函数时的区别

读者到这里有可能会好奇，都是创建函数，那么使用函数声明和函数表达式的区别在哪呢？函数声明不必先声明后使用，先使用后声明也是可以的，例如下面代码也能输出正常值：

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
许多编程语言中的函数，它们的参数和返回值不能是函数。而 JavaScript 中的函数，不仅可以像其他语言一样使用，还可以使用函数作为参数和返回值。这种使用函数作为参数或返回值的函数就叫**高阶函数**，他让 JavaScript 变得更加有魅力，在处理许多复杂运算的时候，可以组合各种函数来完成我们所需的任务。


### 函数作为参数和返回值

我们之前介绍函数参数的时候说道，函数的参数可以是任意类型的数据，函数也是一种数据类型，那么函数就能作为函数的参数。例如下边的代码中的`map`函数就是一个典型的高阶函数，它将数组参数`array`中的成员逐个使用函数参数`fn`加工，然后将加工后的结果放入逐个一个新的数组，根据不同的`fn` `map`能用多种方式处理数据，非常灵活：

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

函数也可以作为返回值，例如，下边代码中的`makeIDGenerator`也是一个高阶函数，它返回了一个每调用一次就递增`1`的函数，实际编程中，我们需要这样的函数来给对象加上递增的`id`，这样`id`不会重复，方便查找和修改：

```javascript
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

之前说到函数的调用，可能大家会觉得似曾相识，实际上，我们在进入这章之前，已经有使用过函数了。例如字符串的`slice`数组的`pop` `push`等等。只不过在当时，我们称它们为「方法」。实际上，函数和方法可谓一脉相承。回忆一下对象一章的知识，我们有学到「对象的属性可以是任意类型的数据」，而函数也是一种数据类型，那么对象的属性实际上也能是函数。那么为了符合面向对象编程的世界观，JavaScript 把这种作为对象属性存在的函数叫做**方法**。

例如下边代码中的对象`user`有一个`sayHiTo`方法：

```javascript
var user = {
  name: 'bella',
  age: 12,
  sayHiTo: function (target) {
    console.log('Hi ~ ' + target);
  }
}

user.sayHiTo('jack'); // 'Hi ~ jack'
```

### this 变量初探

当函数作为某个对象的方法的时候，在它的内部有一个特殊的变量叫`this`这个变量代表着对象本身，例如我们给上边的`user`对象加上一个`selfIntroduction`方法，让它可以进行自我介绍。

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
    this.sayHiTo(target);
    this.selfIntroduction();
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

但是，要吐槽的一点是，`this`不会总是乖乖听话的，例如下边代码中，当我们把方法赋值给某个变量后再运行，`this.name`丢了，而`greetingStart`直接报错。

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

我们知道函数体可以包含各种个样的代码，既然如此，函数体内部就能声明变量，那么

## 函数的练习
1. 使用费马小定理进行素性测试，费马小定理是来自公元 1640 年的一个定理，由数学家费马发现，它的内容是：
  如果 $$ p $$ 是一个素数，那么对于任意的 $$ 1 \le a < p$$  有：
 
 $$ a^{p-1} \equiv 1 \pmod{p} $$
 
 如果我们要测试变量`p`是否为素数，在编程中我们可以按照如下步骤实现
 1. 如果`p <= 1`为`true`那么它不是素数。
 2. 将设定