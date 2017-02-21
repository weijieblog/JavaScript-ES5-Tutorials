## 数组
我们已经学过了字符串、数字和布尔类型的数据，当数据足够简单的时候使用它们已经足够应付。但如果我们想要描述公司某部门的人员名单，菜单上的菜品，博客的留言等**列表**样的数据的时候，使用之前学过的数据类型就会显得繁琐，例如：

```javascript
// 名单
var name1 = '小黄',
    name2 = '小红',
    name3 = '小绿',
    name4 = '小蓝';
    
// 菜单
var dish1 = '宫保鸡丁',
    dish2 = '芹菜牛肉',
    dish3 = '番茄鸡蛋',
    dish4 = '车螺芥菜汤';
    
// 留言
var comment1 = '沙发',
    comment2 = '板凳',
    comment3 = '地板';
```

只看代码可能有些人并不这么认为，但是当名单、菜单和留言是不断变动的情况下问题就会显现出来。比如当我们需要名单上少一个人，菜单上多一个菜品，留言上多几条的时候，又或者我们要对名单、菜单和留言之类的数据进行排序的时候，我们要判断某个人，某个菜品，某条留言是不是在列表里的时候，管理上述多个变量的任务就会变得十分繁琐。这个时候我们就需要学习一种新的数据类型——**数组**，我们可以通过`[]`声明一个数组，如下：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝'];
var menu = ['宫保鸡丁', '芹菜牛肉', '番茄鸡蛋', '车螺芥菜汤'];
var comments = ['沙发', '板凳', '地板'];
```

数组由**成员**组成，例如上文中数组`namelist`中的`'小黄'`, `'小红'`, `'小绿'`, `'小蓝'` 就是数组`namelist`的成员，没有成员的数组叫做**空数组**，我们可以如下声明一个空数组：

```javascript
// 空数组 
var nullList = [];

// 非空数组
var namelist = ['小黄', '小红', '小绿', '小蓝'];
```

成员在数组中的位置，叫做这个成员的**索引**，索引从`0`开始计数，下边的各个表格给出了上边代码中数组 `namelist` `menu``comments`所有成员的索引：

<table>
 <caption><code>namelist</code>的成员及其索引</caption>
 <thead>
  <tr>
   <td><strong>成员</strong></td>
   <td>小黄</td>
   <td>小红</td>
   <td>小绿</td>
   <td>小蓝</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>索引</strong></td>
   <td>0</td>
   <td>1</td>
   <td>2</td>
   <td>3</td>
  </tr>
 </tbody>
</table>

<table>
 <caption><code>menu</code>的成员及其索引</caption>
 <thead>
  <tr>
   <td><strong>成员</strong></td>
   <td>宫保鸡丁</td>
   <td>芹菜牛肉</td>
   <td>番茄鸡蛋</td>
   <td>车螺芥菜汤</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>索引</strong></td>
   <td>0</td>
   <td>1</td>
   <td>2</td>
   <td>3</td>
  </tr>
 </tbody>
</table>

<table>
 <caption><code>comments</code>的成员及其索引</caption>
 <thead>
  <tr>
   <td><strong>成员</strong></td>
   <td>沙发</td>
   <td>板凳</td>
   <td>地板</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>索引</strong></td>
   <td>0</td>
   <td>1</td>
   <td>2</td>
  </tr>
 </tbody>
</table>

与字符串一样，我们可以通过数组的`length`属性获得数组的长度，例如：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝'];
console.log(namelist.length); // 4

var menu = ['宫保鸡丁', '芹菜牛肉', '番茄鸡蛋', '车螺芥菜汤'];
console.log(menu.length); // 4

var comments = ['沙发', '板凳', '地板'];
console.log(comments.length); // 3

var nullList = [];
console.log(nullList.length); // 0
```

## 数组中单个成员的获取和赋值
和字符串一样，数组可以通过成员操作符`[]`取到其中的单个成员，在`[]`取成员的时候，用法和之前字符串介绍的一模一样，例如：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝'];

var first = namelist[0];
console.log(first); // '小黄'

var second = namelist[1];
console.log(second); // '小红'

var a = namelist[0] === namelist['0'] && 
        namelist[1] === namelist['1'] && 
        namelist[2] === namelist['2'];
console.log(a); // true

var b = namelist[1 + 1];
console.log(b); // '小绿'

var last = namelist[namelist.length - 1];
console.log(last); // '小蓝'
```

与字符串不一样的是，在数组中，我们还能够使用赋值操作符`=`对`[]`选取的单个成员进行赋值，例如：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝'];
console.log(namelist[0]); // '小黄'

// 给数组 namelist 的第一个成员赋值
namelist[0] = '小紫';
console.log(namelist[0]); // '小紫'
console.log(namelist); // ['小紫', '小红', '小绿', '小蓝']

// 给数组 namelist 的最后一个成员赋值
namelist[namelist.length - 1] = '小白';
console.log(namelist[namelist.length - 1]); // '小白'
console.log(namelist); // ['小紫', '小红', '小绿', '小白']
```

## 操作数组
JavaScript 提供了许多方法帮我们方便的增加、删除、修改、查找数组的成员，下面介绍部分常用的方法。

### 使用`indexOf`获取数组成员的索引

与字符串类似，JavaScript 的数组提供了`indexOf`方法帮助我们方便的获取数组某个成员的索引，例如，当我们需要从数组`namelist`中得到成员`'小绿'`的索引：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝'];
var index = namelist.indexOf('小绿');
console.log(index); // 2
console.log(namelist[index]); // '小绿'
```

`indexOf` 方法返回第一个找到的数组成员的索引，如果数组中有多个`'小绿'`得到的也还是第一个`'小绿'`的索引，例如：

``` javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小绿', '小白'];
var index = namelist.indexOf('小绿');
console.log(index); // 2
```

如果我们想要得到第二个`'小绿'`的索引，我们可以通过`indexOf`的第二个参数，设置开始查找的位置，例如我们让 `indexOf`从跳过第一个`'小绿'`，从`'小蓝'`的位置找起：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小绿', '小白'];
var index = namelist.indexOf('小绿', 3); // 这里的 3 是'小蓝'的索引，就相当于告诉 indexOf 从'小蓝'的位置开始寻找
console.log(index); // 4
```

如果我们想从`namelist`中得到多个`'小绿'`的位置，我们可以动态的设置`indexOf`的第二个参数，例如：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小绿', '小白'];
var firstIndex = namelist.indexOf('小绿');
// 我们知道 firstIndex 是第一个'小绿'的索引
// 所以 firstIndex + 1 就是告诉 JavaScript 从第一个'小绿'的后面一个位置开始找起
var secondIndex = namelist.indexOf('小绿', firstIndex + 1);
console.log(firstIndex, secondIndex); // 2 4
```

最后还有一种情况，就是如果数组中没有我们想找的成员，则`indexOf`会返回`-1`，例如：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小绿', '小白'];
var index = namelist.indexOf('二狗子');
console.log(index); // -1
index = namelist.indexOf('二狗子', 3);
console.log(index); // -1
```

因此我们就可以通过逻辑表达式判断某个成员是否属于当前数组了，例如：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小绿', '小白'];
var isContain = namelist.indexOf('小红') !== -1;
console.log(isContain); // true

isContain = namelist.indexOf('二狗子') !== -1;
console.log(isContain); // false
```

### 使用`splice`方法在数组的指定位置删除和添加成员

通过数组的`splice`方法我们可以在数组任意位置追加或者删除成员，例如下列代码从数组`namelist`中移除成员`'小绿'`：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小白'];
var index = namelist.indexOf('小绿');

console.log(namelist[index]); // '小绿'

// 第一个参数 index 为'小绿'在数组 namelist 中的索引
// 第二个参数 1 告诉 splice 只删除一个成员
namelist.splice(index, 1);
console.log(namelist); // ['小黄', '小红', '小蓝', '小白']
```
`splice`方法的第一个参数是修改操作开始位置的索引，例如上边代码中的`index`标记了成员`'小绿'`的位置，第二个参数是要删除成员的数量，我们写了`1`表示只删除一个成员，因此如果我们想要删除多个成员就可以修改第二个参数，例如下面的代码从数组`namelist`中删除了`'小红'`, `'小绿'`, `'小蓝'`三个成员：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小白'];
var index = namelist.indexOf('小红');

console.log(namelist[index]); // '小红'

// 第一个参数 index 为'小红'在数组 namelist 中的索引
// 第二个参数 3 告诉 splice 删除三个成员
namelist.splice(index, 3);
console.log(namelist); // ['小黄', '小白']
```

如果我们使用`splice`方法删除了数组中的成员，它的返回值就是被删除的成员组成的数组，例如：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小白'];
var index = namelist.indexOf('小红');
var result = namelist.splice(index, 1); // 这里的 result 就是返回值
console.log(result); // ['小红'] ，注意返回的是个数组

var menu = ['宫保鸡丁', '芹菜牛肉', '番茄鸡蛋', '车螺芥菜汤'];
index = menu.indexOf('芹菜牛肉');
result = menu.splice(index, 2);
console.log(result); // ['芹菜牛肉', '番茄鸡蛋']
```

同时`splice`方法允许我们向数组中插入成员，例如下面代码在数组`namelist`的成员`'小红'`之前插入两个成员`'小猫'`和`'小狗'`：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小白'];
var result = namelist.splice(1, 0, '小猫', '小狗');
console.log(namelist); // ['小黄', '小猫', '小狗', '小红', '小绿', '小蓝', '小白']
console.log(result); // [] 空数组，因为 splice 的第二个参数是 0 所以没有成员被删除
```

上边的代码告诉`splice`，修改的开始位置的索引是`1`，删除`0`个成员，并在索引`1`之前插入两个成员`'小猫'`和`'小狗'`。
如此一来，我们就可以通过设置`splice`的参数来编辑数组的成员，例如下列代码将数组`namelist`中的`'小红'`和`'小绿`替换为`'小猫'`、`'小狗'`和`'小猪'`：


```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小白'];

// 从索引为 1 的地方开始修改，删除 2 个成员，并插入三个成员'小猫'、'小狗'和'小猪'
var result = namelist.splice(1, 2, '小猫', '小狗', '小猪');

console.log(namelist); // ['小黄', '小猫', '小狗', '小猪', '小蓝', '小白']
console.log(result); // ['小红'， '小绿']
```

### 向数组的开头或者末尾删除和添加成员
虽然`splice`方法已经能够让我们操作数组任意位置的成员，但是在实际开发中，我们经常需要向数组的开头或者末尾删除和添加成员，每次都用`splice`未免有些繁琐，因此 JavaScript 提供了一些便捷的方法让我们使用。

#### 使用`push`和`pop`方法向数组的末尾追加或者删除一个成员
`push`方法向数组的末尾追加一个成员，它只接受一个参数，即需要追加的成员，返回值是数组的长度，例如：

```javascript
var menu = [];
var len = menu.push('白灼虾');
console.log(menu, len); // ['白灼虾'] 1

len = menu.push('酸甜排骨');
console.log(len); // 2

len = menu.push('清蒸鲈鱼');
console.log(menu, len); // ['白灼虾', '酸甜排骨', '清蒸鲈鱼'] 3
```

`pop`方法向数组的末尾删除一个成员，它没有参数，返回值是被删除的成员，例如：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小白'];
var poped = namelist.pop();
console.log(namelist, poped); // ['小黄', '小红', '小绿', '小蓝'] '小白'

poped = namelist.pop();
console.log(namelist, poped); // ['小黄', '小红', '小绿'] '小蓝'
```

#### 使用`shift`和`unshift`方法向数组的开头添加或删除一个成员
`unshift`方法向数组的开头追加一个成员，它只接受一个参数，即需要追加的成员，返回值是数组的长度，例如：

```javascript
var menu = [];
var len = menu.unshift('白灼虾');
console.log(menu, len); // ['白灼虾'] 1

len = menu.unshift('酸甜排骨');
console.log(len); // 2

len = menu.unshift('清蒸鲈鱼');
console.log(menu, len); // ['清蒸鲈鱼', '酸甜排骨', '白灼虾'] 3
```

`shift`方法向数组的开头删除一个成员，它没有参数，返回值是被删除的成员，例如：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小白'];
var shifted = namelist.shift();
console.log(namelist, shifted); // ['小红', '小绿', '小蓝', '小白'] '小黄'

shifted = namelist.shift();
console.log(namelist, shifted); // ['小绿', '小蓝', '小白'] '小红'
```

## 数组拼接和切片
数组也可以像字符串一样进行拼接和切片的操作。

### 使用`concat`方法拼接数组

我们知道在字符串类型的数据里，我们可以使用`+`拼接两个字符串。类似的，在数组里我们可以使用`concat`方法拼接两个数组，例如：

```javascript
var a = [1, 2, 3],
    b = [4, 5];
   
var c = a.concat(b);
console.log(c); // [1, 2, 3, 4, 5]
```

`concat`方法并不会改变数组本身，例如我们将数组`a`和数组`b`拼接后的结果赋值给变量`c`，数组`a`和`b`并没有任何变化：

```javascript
var a = [1, 2, 3],
    b = [4, 5];
   
var c = a.concat(b);
console.log(a); // [1, 2, 3]
console.log(b); // [4, 5]
console.log(c); // [1, 2, 3, 4 ,5]
```

如果想同时拼接多个数组可以按照如下方式使用`concat`：

```javascript
var a = [1, 2],
    b = [3, 4],
    c = [5, 6],
    d = [7, 8];

var e = a.concat(b.concat(c.concat(d)));
console.log(e); // [1, 2, 3, 4, 5, 6, 7, 8]
```


### 使用`slice`对数组进行切片

数组也提供了`slice`方法，用法和字符串的`slice`一模一样，例如：

```javascript
var namelist = ['小黄', '小红', '小绿', '小蓝', '小白'];

var a = namelist.slice(0,3),
    b = namelist.slice(0, namelist.length - 1),
    c = namelist.slice(2);
    
console.log(a); // ['小黄', '小红', '小绿']
console.log(b); // ['小黄', '小红', '小绿', '小蓝']
console.log(c); // ['小绿', '小蓝', '小白']
```

## 数据的复合类型和基础类型

上文中我们已经见过了许多成员为字符串的的数组，那是为了叙述方便，其实数组的成员可以是**任何类型**的数据，注意是**任何类型**，包括我们已经学了的数据类型和还没学的数据类型，例如下边代码声明了由我们已经学过的数据类型为成员的数组：

```javascript
// 字符串类型，描述公司某部门的人员名单
var namelist = ['小黄', '小红', '小绿', '小蓝', '小白'];

// 数字类型，斐波那契数列的前几位
var fibonacci = [1, 1, 2, 3, 5, 8, 13, 21, 34];

// 布尔类型，描述某道判断题的答案
var answers = [false, true, false, false, true];
```

同一个数组的不同成员也可以是不同的数据类型，例如：

```javascript
var a = [1, false, '西瓜', true, 2334];
console.log(a[0]); // 1
console.log(a[1]); // false
console.log(a[2]); // '西瓜'
```

我们可以看到，数组的成员可以是各种类型的数据，而这些成员一并组成了数组。像数组这种可以由多种数据类型成员组合而成的数据类型，叫做**复合类型**。而像字符串，数字，布尔值这种单一的数据类型，叫做**基础类型**。复合类型由基础类型的数据组合而成，就像数组的成员，可以是各种字符串，数字，布尔值一样。

## 二维数组
前面说到数组成员可以是任何类型的数据，所以，数组的成员也可以是数组，例如：

```javascript
var a = [
  [1,2,3],
  [4,5,6],
  [7,8,9]
];

console.log(a[0]); // [1,2,3]
console.log(a[1]); // [4,5,6]
console.log(a[2]); // [7,8,9]
```

像这种成员为数组的数组，我们把它叫做二维数组，可以把它们想象成为一张二维表，例如上边的代码的数组`a`就描述了下表：

<table>
 <tbody>
  <tr>
   <td>1</td>
   <td>2</td>
   <td>3</td>
  </tr>
  <tr>
   <td>4</td>
   <td>5</td>
   <td>6</td>
  </tr>
  <tr>
   <td>7</td>
   <td>8</td>
   <td>9</td>
  </tr>
 </tbody>
</table>

上边的示例已经通过`a[0]`、`a[1]`和`a[2]`取到了数组`a`的三个成员，这些成员都是数组，可以吧它们想象为上述表的行，如果我们想要取到具体某个单元格的值，可以如下操作，例如下边代码取到了`3` `5` `7`。

```javascript
var a = [
  [1,2,3],
  [4,5,6],
  [7,8,9]
];

var firstRow = a[0]; // 取到表格的第 0 行
console.log(firstRow); // [1,2,3]
console.log(firstRow[2]); // 3

var secondRow = a[1]; // 取到表格的第 1 行
console.log(secondRow); // [4,5,6]
console.log(secondRow[1]); // 5

var thirdRow = a[2]; // 取到表格的第 2 行
console.log(thirdRow); // [7,8,9]
console.log(thirdRow[0]); // 7
```

其实我们不必每行都保存到变量里，可以直接通过坐标访问到具体单元格的值，下方是加了坐标系的二维表。


<table>
 <tbody>
  <tr>
   <td>y\x</td>
   <td>0</td>
   <td>1</td> 
   <td>2</td>  
  </tr>
  <tr>
   <td>0</td>
   <td>1</td>
   <td>2</td>
   <td>3</td>
  </tr>
  <tr>
   <td>1</td>
   <td>4</td>
   <td>5</td>
   <td>6</td>
  </tr>
  <tr>
   <td>2</td>
   <td>7</td>
   <td>8</td>
   <td>9</td>
  </tr>
 </tbody>
</table>

上述代码中`firstRow ``secondRow ``thirdRow`它们都是数组类型的数据，我们通过形如`a[y]`的表达式得到了它们，也就是说`a[y]`的表达式的返回值是个数组类型的数据，因此我们可以再对`a[y]`的返回值使用成员操作符`[]`。那么我们就可以直接通过`a[y][x]`获取到具体的单元格的值，比如我们获取数组`a`中的`2``4``8`：

```javascript
var a = [
  [1,2,3],
  [4,5,6],
  [7,8,9]
];

console.log(a[0][1]); // 2
console.log(a[1][0]); // 4
console.log(a[2][1]); // 8
```
同样的我们还可以通过`[][]`对二维数组的成员进行赋值，如下：

```javascript
var a = [
  [1,2,3],
  [4,5,6],
  [7,8,9]
];

console.log(a[0][1]); // 2
a[0][1] = 0;
console.log(a[0][1]); // 0
```
这么一来，二维表就变成了下面这样：

<table>
 <tbody>
  <tr>
   <td>1</td>
   <td>0</td>
   <td>3</td>
  </tr>
  <tr>
   <td>4</td>
   <td>5</td>
   <td>6</td>
  </tr>
  <tr>
   <td>7</td>
   <td>8</td>
   <td>9</td>
  </tr>
 </tbody>
</table>

这世界上有二维数组，就有三位数组，四维数组，它们只是听起来可怕，但实际的原理都和二维数组一样。成员都是一维数组的数组是二维数组，成员都是二维数组的数组是三维数组，成员都是三维数组的数组是四维数组，以此类推。

## 数组练习

1. 声明一个数组，由成员`'鸡蛋'`、`'肉类'`、`'果汁'`、`'麦片'`、`'牛奶'`组成。
2. 声明一个数组，由成员`3`、`1`、`4`、`1`、`5`组成。
3. 根据下面的数组回答问题：
 
 ```javascript
 var collection = ['沉沦', '春风沉醉的晚上', '过去', '采石矶', '茫茫夜'];
 ```
  * a. 成员`'采石矶'`的索引是什么。
  * b. 写代码通过成员操作符将`'春风沉醉的晚上'`改成`'茑萝行'`。
  * c. 写代码通过成员操作符取到`'过去'`。
  * d. 写代码取到该数组的长度。
4. 根据下面的数组回答问题：

 ```javascript
 var menu = ['薯条', '炸鸡', '可乐', '烤翅', '圣代'];
 ```
 
 * a. 成员`'炸鸡'`的索引是什么？
 * b. 写代码通过成员操作符将`'炸鸡'`改成`'烤鸡'`。
 * c. 写代码通过成员操作符和`length`属性，取到数组的最后一个成员`'圣代'`。
 * d. 写代码用过成员操作符和`length`属性，将数组的最后一个成员改成`'甜筒'`。
 
5. 使用`indexOf`方法根据下面的数组回答问题：

 ```javascript
 var fruits = ['雪梨', '苹果', '香蕉', '西瓜', '苹果', '柑果'];
 ```
 
 * a. 写出取到成员`'香蕉'`索引的代码。
 * b. 写出取到第二个`'苹果'`索引的代码。
 * c. 写出取到两个`'苹果'`索引的代码。

6. 使用`indexOf`方法根据下面的数组回答问题：

 ```javascript
 var numbers = [23, 32, 455, 66546, 43, 32, 65, 32, 56];
 ```
 
 * a. 写出取到成员`66546 `索引的代码。
 * b. 写出取到第三个`32`索引的代码。
 * c. 写出取到所有`32`索引的代码。
 
7. 使用`splice`方法根据下面的数组回答问题：

 ```javascript
 var namelist = ['Jognny', 'Lori', 'Quadro', 'Hank', 'Collin', 'Roberta'];
 ``` 
 * a. 写出从中删除`'Quadro'`的代码。
 * b. 写出从中删除`'Lori'``'Quadro'``'Hank'`的代码。
 * c. 写出在`'Lori'`前插入`'Lily'``'Bella'`的代码。
 * d. 将原数组中的`'Hank'``'Collin'``'Roberta'`改为`'Lily'``'Bella'`。
 
8. 使用`splice`方法根据下面的数组回答问题：
 
 ```javascript
 var codes = [3, 1, 4, 1, 5, 9, 2, 6, 5];
 ```
 
 * a. 写出从中删除第一个`1`的代码。
 * b. 写出从中删除`1``4``1`的代码。
 * c. 写出在最后插入`3``5`的代码。
 * d. 将原数组中的`5``9``2``6``5`改为`6`。
 
9. 当运行下列代码时，`#a~#e`各输出什么。

 ```javascript
 var list = [], l;
 list.push('Saturday');
 console.log(list); // #a
 
 l = list.push('Sunday');
 console.log(list); // #b
 console.log(l); // #c
 
 console.log(list.pop()); // #d
 console.log(list); // #e
 ```
 
10. 当运行下列代码时，`#a~#e`各输出什么。
 
 ```javascript
 var list = [], l;
 list.unshift('Tuesday');
 console.log(list); // #a
 
 l = list.unshift('Monday');
 console.log(list); // #b
 console.log(l); // #c
 
 console.log(list.shift()); // #d
 console.log(list); // #e
 ```
 
11. 使用`unshift``shift``push``pop`方法根据下列数组回答问题：
 
 ```javascript
 var one = ['Wednesday'];
 var two = ['Monday', 'Wednesday', 'Friday'];
 var three = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
 ```
 
 * a. 写出将数组`one`转变为数组`two`的代码。
 * b. 写出将数组`two`转变为数组`one`的代码。
 * c. 写出将数组`two`转变为数组`three`的代码。
 
12. 使用`concat`方法拼接数组。
  
  ```javascript
  var a = [1, 2],
      b = [2, 3],
      c = [3, 4];
      
  var d = [];
  ```
  
  * a. 写出将数组`a`和数组`a`拼接的代码。
  * b. 写出将数组`a``b``c`拼接到一起的代码。
  * c. `a.concat(d)`的结果是什么？
  
13. 使用`slice`方法根据俄下列数组对回答问题。

 ```javascript
 var days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
 ```
 
 * a. `days.slice(0)`的结果是什么？
 * b. 写出从`days`中取得`['Tuesday', 'Wednesday', 'Thursday']`的代码。
 * c. 写出从`days`中取得`['Friday', 'Saturday']`的代码。
 
 
14. 根据下表回答问题。

   <table>
    <tbody>
     <tr>
      <td>1</td>
      <td>2</td>
      <td>3</td>
     </tr>
     <tr>
      <td>2</td>
      <td>2</td>
      <td>3</td>
     </tr>
     <tr>
      <td>3</td>
      <td>2</td>
      <td>3</td>
     </tr>
     <tr>
      <td>4</td>
      <td>2</td>
      <td>3</td>
     </tr>
    </tbody>
   </table>
 
 * a. 使用二维数组描述上面表格。
 * b. 通过成员操作符修改 a 小题得到的二维数组，使之能够描述下列表格。
   
     <table>
      <tbody>
       <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
       </tr>
       <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
       </tr>
       <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
       </tr>
       <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
       </tr>
      </tbody>
     </table>

  * c. 通过本章学习的方法修改 b 小题得到的数组，随便删掉表格的一行，使之能够描述下列表格。

     <table>
      <tbody>
       <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
       </tr>
       <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
       </tr>
       <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
       </tr>
      </tbody>
     </table>

15. 根据下表回答问题。

     <table>
      <tbody>
       <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
       </tr>
       <tr>
        <td>4</td>
        <td>5</td>
        <td>6</td>
       </tr>
      </tbody>
     </table>
   
   * a. 使用二维数组描述上面表格。
   * b. 给 a 小题得到的二维数组增加一行，使之能够描述下列表格   
   
     <table>
      <tbody>
       <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
       </tr>
       <tr>
        <td>4</td>
        <td>5</td>
        <td>6</td>
       </tr>
       <tr>
        <td>7</td>
        <td>8</td>
        <td>9</td>
       </tr>
      </tbody>
     </table>
   
   * c. 通过成员操作符修改 b 小题得到的二维数组，使之能够描述下列表格。
   
     <table>
      <tbody>
       <tr>
        <td>1</td>
        <td>0</td>
        <td>3</td>
       </tr>
       <tr>
        <td>4</td>
        <td>0</td>
        <td>6</td>
       </tr>
       <tr>
        <td>7</td>
        <td>0</td>
        <td>9</td>
       </tr>
      </tbody>
     </table>
