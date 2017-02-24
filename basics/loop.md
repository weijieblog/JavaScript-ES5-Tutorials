## 循环语句

在现实编程中，我们会被要求一次性渲染一百条留言到页面上，从有一万个用户的数组中筛选出符合要求的用户，一次性改变页面中十多个按钮的颜色等等。当我们需要执行类似不断重复机械的任务的时候，就可以使用循环语句。JavaScript 提供了三种不同的循环语句供我们使用，它们分别是`while`语句、`do...while`语句和`for`语句。下边将逐个介绍这三个循环语句的用法。

## while 语句
### while 语句的使用
`while`语句是最简单的循环语句，语法如下边伪代码描述：

```
while(条件) {
  循环体
}
```

上边伪代码中的「条件」和条件语句中介绍的一致，循环语句中的代码块叫做**循环体**，可以包含任意的代码。`while`语句先对「条件」进行判断，如果「条件」的结果为假，不执行循环体中的代码，如果「条件」的结果为真，执行循环体中的代码；执行完后，再次判断「条件」的真假，为真就再次执行循环体中的代码，为假就不执行，如此往复。

在 JavaScript 中，我们就可以这样使用`while`语句，例如，下列代码在控制台输出`1~10`：

```javascript
var i = 1;
while(i <= 10) {
  console.log(i);
  i++;
}
```
> 上面`while`语句的执行步骤如下
> 1. 判断「条件」的真假，如果 `i <= 10` 为`true` 就执行步骤 2 3 4，为`false`就不执行
> 2. 执行`console.log(i)`
> 3. 执行`i++`（注意：`i`的增长迟早会让`i <= 10`的返回值为`false`以结束掉循环）
> 4. 回到步骤 1

### 死循环

有这么一种情况，循环语句中的「条件」的结果一直为真，那么程序就会永无休止的执行循环体的内容，这种循环叫**死循环**。多数情况下，死循环会导致程序卡死，例如下面的代码会永无休止的在控制台输出`1`：

```javascript
var i = 1;
while(i <= 10) {
  console.log(i);
  // 注释掉了 i++ 让，i 不再增长则 i <= 10 的返回值永远为 true
  // i++; 
}
```
> 强烈推荐执行上边的代码，体验一下什么叫程序卡死。

### break 语句在循环中的使用

在所有循环语句中都能使用`break`语句，在循环语句中使用`break`语句可以提前跳出循环，例如下边的代码在`i`的值为`5`的时候跳出这个循环：

```javascript
var i = 1;

// 在控制台中输出 1 2 3 4
while(i <= 10) {
  if (i === 5){
    break; // #1
  } 
  console.log(i);
  i++; 
}
// #2
```
> 当`#1`处的`break`被执行后程序会直接跳转到`#2`处。

### continue 语句在循环中的使用

我们知道，通常情况下循环体中的代码会被一轮又一轮的执行，但有的时候我们希望结束这一轮循环，提前进入下一轮，我们就可以使用`continue`语句，例如下边的代码在`i`的值为`3` `5` `7`的时候提前结束了当前轮循环，进入下一轮（如果有的话）：

```javascript
var i = 1;

// 在控制台中输出 1 2 4 6 8 9 10，即没有输出 3 5 7
while(i <= 10) { // #2
  if (i === 3 || i === 5 || i === 7){
    i++;
    continue; // #1
  }
  console.log(i);
  i++;
}

```
> 当`#1`处的`continue`被执行后，程序会跳转到`#2`处重新判断`i <= 10`的返回值，
> 如果为`true`则执行循环体中的代码，如果为`false`则不执行。

## do...while 语句

### do...while 语句的使用
`do...while`语句的语法如下伪代码描述：

```
do {
  循环体
} while(条件);
```
`do...while`语句首先执行循环体中的内容，然后判断「条件」的结果，如果结果为真就再次执行循环体中的内容，如果结果为假语句就结束，如此往复。例如，下列代码在控制台中输出`1~10`：

```javascript
var i = 1;
do {
  console.log(i);
  i++;
} while(i <= 10);
```
> 上面`do...while`语句的执行步骤如下
> 1. 执行`console.log(i)`
> 2. 执行`i++`（注意：`i`的增长迟早会让`i <= 10`的返回值为`false`以结束掉循环）
> 3. 判断`i <= 10`的返回值，如果为`true` 就回到步骤 1，为`false`语句结束

### do...while 语句和 while 语句的区别
`do...while`语句和`while`语句长得类似，实际上它们略有区别，它们的区别如下：

1. `do...while`语句先执行循环体中的内容，再判断条件是否成立，成立则再执行，不成立则结束。
2. `while`语句则先判断条件是否成立，成立则执行循环体中的内容。

简单说来，`do....while`是先斩后奏，`while`是先奏后斩。当条件都不成立的时候，`do....while`能够至少执行一次循环体，`while`的循环体则一次也不会被执行：

```javascript
var i = 1;

while (i > 999){
  console.log('我一次都没被执行');
  i++;
}


do {
  console.log('我执行了一次');
  i++;
} while(i > 999);
```

为什么是「至少执行一次」，是因为有一种情况，一开始条件不成立，但执行一次循环体后，条件成立了，那么这个时候，使用`do....while`语句就不只是执行一次，而是执行多次，所以说`do....while`能够「至少执行一次」。例如下边代码中`do....while`能够输出`0~10`而`while`语句则什么都不输出：

```javascript
var i = 0;

// 条件 i > 0 && i <= 10 不成立
// 则循环体的代码不被执行
while (i > 0 && i <= 10){
  console.log(i);
  i++;
}

var j = 0;

// 一开始条件 i > 0 && i <= 10 不成立
// 但执行一次循环体后成立了
// 于是循环体的代码被执行多次
do {
  console.log(j);
  j++;
} while(j > 0 && j <= 10);
```

当条件一开始都成立，则差不多，反正都是斩，前奏后奏区别不大，例如下边两个循环语句都能输出`1~10`：

```javascript
var i = 1;
do {
  console.log(i);
  i++;
} while(i <= 10);

var j = 1;
while(j <= 10) {
  console.log(j);
  j++;
}
```

## for 语句

### for 语句的使用

先人们发现，虽然`while`语句做到循环也不怎么麻烦，但是大多数使用`while`语句的时候，都是这样的：

```
先定义一个条件

while(判断条件是否成立) {
  循环体的代码
  
  在循环体的结尾，持续的改变条件，让循环可以退出
}
```
不信你看这个在控制台输出`1~10`的例子：

```javascript
var i = 1; // 先定义一个条件
while(i <= 10) { // 判断条件是否成立
  console.log(i);
  i++; // 在循环体的结尾，持续的改变条件，让循环可以退出
}
```

然后先人们觉得总是这样太麻烦了，就发挥了程序员不惜一切代价偷懒的精神发明了`for`语句，让各个步骤可以写在一行，于是`for`语句就成了这世界上最最最常用的循环语句，`for`语句的语法如下伪代码描述：

```
for(定义一个条件; 判断条件是否成立; 持续的改变条件) {
  循环体
}
```
 `for`语句执行的步骤如下：
 
 1. 首先「定义一个条件」。
 2. 然后「判断条件是否成立」，如果成立，则执行步骤 3 4 5，不成立则语句结束。
 3. 执行循环体的内容
 4. 执行「持续的改变条件」。
 4. 回到步骤 2。


所以在控制台输出`1~10`的例子用`for`语句写出来如下：

``` javascript
for (var i = 1; i <= 10; i++) {
  console.log(i);
}
```

> 上边`for`语句的执行步骤如下
> 1. 首先执行`var i = 1`。
> 2. 然后判断`i <= 10`的返回值是否为`true`，为`true`就执行步骤 3 4 5，否则语句结束。
> 3. 执行`console.log(i)`。
> 4. 执行`i++`。
> 5. 回到步骤 2

### 使用 for 语句操作数组

#### 数组的遍历
有的时候，我们需要访问数组中的所有成员，就可以使用`for`语句从头到位访问挨个访问数组的各个成员，这种操作叫做**数组的遍历**。例如下列的代码在控制台上挨个输出了数组`users`的全部成员：

```javascript
var users = [
  {name: '李约翰', age: 27, gender: 'male'},
  {name: '柳丽文', age: 33, gender: 'female'},
  {name: '章文武', age: 19, gender: 'male'},
  {name: '王柳', age: 20, gender: 'female'},
  {name: '莫梦琳', age: 56, gender: 'female'},
  {name: '山本冈昌', age: 28, gender: 'male'},
];

for (var i = 0; i < users.length; i++) {
  console.log(users[i]); // #1
}
```
> 上边的代码有如下要注意的地方，
> 
> 1. `var i = 0`让`i`的值一开始为`0`。
> 1. 通过`i < users.length`限制`i`的最大值在这个语句中只能是`users.length - 1`。
> 3. `i++`让`i`的值从一开始的`0`增长到`users.length -1`。
> 4. 于是`#1`处的`users[i]`就可以从数组的第一个成员（`users[0]`）访问到数组的最后一个成员（`users[users.length-1]`）。

#### 使用数组的遍历
知道了如何遍历一个数组，我们就可以对数组进行复杂的操作了。例如，下列代码将数列`numbers`进行求和：

```javascript
var numbers = [1, 3, 5, 6, 2, 21, 2];

var result = 0;
for (var i = 0; i < numbers.length; i++) {
  result += numbers[i];
}
console.log(result); // 40
```

也可以对数组的成员进行筛选，例如，下列代码找选出了数组`users`中年龄大于等于三十的成员：

```javascript
var users = [
  {name: '李约翰', age: 27, gender: 'male'},
  {name: '柳丽文', age: 33, gender: 'female'},
  {name: '章文武', age: 19, gender: 'male'},
  {name: '王柳', age: 20, gender: 'female'},
  {name: '莫梦琳', age: 56, gender: 'female'},
  {name: '山本冈昌', age: 28, gender: 'male'},
];

var result = [];
for (var i = 0; i < users.length; i++) {
  if (users[i].age >= 30) {
    result.push(users[i]);
  }
}
console.log(result); // [{name: '柳丽文', age: 33, gender: 'female'}, {name: '莫梦琳', age: 56, gender: 'female'}]
```

也可以通过名字删除成员，例如从数组`users`中删掉名字叫`'山本冈昌'`的成员：

```javascript
var users = [
  {name: '李约翰', age: 27, gender: 'male'},
  {name: '柳丽文', age: 33, gender: 'female'},
  {name: '章文武', age: 19, gender: 'male'},
  {name: '王柳', age: 20, gender: 'female'},
  {name: '莫梦琳', age: 56, gender: 'female'},
  {name: '山本冈昌', age: 28, gender: 'male'},
];

for (var i = 0; i < users.length; i++) {
  if (users[i].name === '山本冈昌') {
    users.splice(i, 1);
  }
}
console.log(users); 
```

过了一年，给数组`users`中的每个成员的年龄都加一：

```javascript
var users = [
  {name: '李约翰', age: 27, gender: 'male'},
  {name: '柳丽文', age: 33, gender: 'female'},
  {name: '章文武', age: 19, gender: 'male'},
  {name: '王柳', age: 20, gender: 'female'},
  {name: '莫梦琳', age: 56, gender: 'female'},
  {name: '山本冈昌', age: 28, gender: 'male'},
];

for (var i = 0; i < users.length; i++) {
  users[i].age += 1;
}
console.log(users); 
```

等等等等。

### for...in 语句

在 JavaScript 中`for..in`语句是种特殊的`for`语句，大多数情况下，它的功能只有一个，就是遍历一个对象，例如下列代码逐个输出了对象的属性名和属性值：

```javascript
var book = {
  title: '双城记',
  author: '狄更斯',
  years: 1859
};

for(var key in book) {
  console.log(key, book[key]);
}
```
与操作遍历数组类似，我们能够遍历一个对象了以后，也可以对对象进行复杂的操作。比如下列代码获取了对象`book`的全部属性名，存放在数组`result`中：

```javascript
var book = {
  title: '双城记',
  author: '狄更斯',
  years: 1859
};

var result = [];
for(var key in book) {
  result.push(key);
}

console.log(result); // ['title', 'author', 'years']
```

## 嵌套循环

我们已经学过了如何使用循环语句来遍历单个的对象或者数组，但是有的时候，我们需要处理一些更复杂的情况，比如遍历二维数组，遍历属性是数组的对象中每个属性的成员，成员是对象的数组中每个成员的属性，如此一来单个的循环语句就有些使不上力了，我们需要组合使用多个循环语句，例如下边的代码从二维数组`animals`中找到`'恐龙'`的坐标：

```javascript
var animals = [
  ['白兔', '老鼠', '食蚂兽'],
  ['蛇', '蜥蜴', '恐龙'],
  ['鸡', '老鹰', '八哥']
];

var x, y;

for (var i = 0; i < animals.length; i++) { // #1
  for (var j = 0; j < animals[i].length; j++) {  // #2
    if (animals[i][j] === '恐龙') {
      x = i;
      y = j;
    }
  }
}

console.log(animals[x][y]); // 恐龙
```
>  `#1`处的第一层循环会逐个访问`animals`中的每个成员，由于每个成员又是数组，所以`#2`处的第二层循环遍历`animals`成员的成员。

当对象的属性是数组的时候，我们也可以参照上面的方法嵌套`for..in`语句和`for`语句，例如下面的代码从对象`animals`中找到`'恐龙'`：

```javascript
var animals = {
  suckler: ['白兔', '老鼠', '食蚂兽'],
  reptilian: ['蛇', '蜥蜴', '恐龙'],
  birds: ['鸡', '老鹰', '八哥']
};

var x, y;

for (var key in animals) { // #1
  for (var j = 0; j < animals[key].length; j++) {  // #2
    if (animals[key][j] === '恐龙') {
      x = key;
      y = j;
    }
  }
}

console.log(animals[x][y]); // 恐龙
```
>  因为`animals`是个对象所以`#1`处的第一层循环使用`for...in`语句，`#2`处的第二层循环遍历`animals`属性（是个数组）的成员。

## 循环语句练习

1. 有一个数组`nums`，写代码将每个成员平方。

    ```
    var nums = [2, 4, 6, 8, 9];
    「你写的代码」
    console.log(nums); // [4, 16, 36, 64, 81]
    注意，无论数组成员的数量有多少，每个成员的大小是多少「你写的代码」依然要能够正常工作
    ```
    * a. 使用`while`语句完成代码
    * b. 使用`do...while`语句完成代码
    * c. 使用`for`语句完成代码

2. 欧几里得算法是一种求最大公约数的数值算法，最早出现于欧几里得的《几何原本》中。我们要求$$a$$和$$b$$的最大公约数，我们可以按照如下步骤计算：
  1. 将$$a$$ $$b$$分别赋值给变量`n` `m`。
  1. 判断`m`是否为`0`，如果为`0`那么此时`n`就是最大公约数，如果不为`0`就执行以下步骤
  2. 将`m`赋值给变量`t`
  3. 将`n % m`赋值给变量`m`
  4. 将`t`赋值给变量`n`
  5. 回到步骤 2
  
    ```
    求 12 28 的最大公约数
    var n = 12, m = 28;
    「你写的代码」
    console.log(n); // 4
    ```  
3. 写代码将分数约分。提示：将分子和分母赋值给两个变量，然后使用欧几里得算法求得分子和分母的最大公约数，然后分子分母同除以最大公约数，就完成了分数的约分。

    ```
    将分数 12／28 约分
    var n = 12, m = 28;
    「你写的代码」
    console.log(n, m); // 3 7
    ```