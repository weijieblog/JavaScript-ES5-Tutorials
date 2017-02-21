## 对象
在实际的开发中，我们经常要面对用户提交的表单数据，服务器传来的用户信息数据，服务器传来的书本数据等等数据。这些数据都是由多个值组成的，比如用户提交的数据中包含「账户名」、「密码」，服务器传来的用户数据包含该用户的「名字」、「性别」、「年龄」，书本数据中包含该书的「作者」、「书名」、「出版年代」。当我们需要描述这种由多个值构成的数据时，就会用到**对象**这种数据类型。
JavaScript 通过`{}`声明一个对象，比如下面的代码中我们声明了对象`authInfo``user``book`分别描述一个用户的登录信息、用户信息和一本书的信息。

```javascript
// authInfo 对象，描述登录信息
var authInfo = {
  username: 'Andy',  // 用户名
  password: '123456' // 密码
};

//user 对象，描述用户信息 
var user = {
  name: 'Tony',       // 名字
  age: 20,            // 年龄
  gender: 'male'      // 性别
};

// book 对象，书本信息
var book = {
  title: 'A Tale of Two Cites',   // 书名
  author: 'Charles Dickens',      // 作者
  years: 1859                     // 出版年代
};
```

对象由**属性**组成，例如上面代码中的对象`book`就有三个属性，它们的**属性名**分别是`title``author``years`是字符串。而在对象中属性的值叫**属性值**，比如对象`book`中，属性名为`title`的属性的属性值是`'A Tale of Two Cites'`，属性名为`author`的属性的属性值是`'Charles Dickens'`，属性名为`years`的属性的属性值是`1859`。

在声明对象时，碰到属性名格式比较特殊的情况（多数情况下是属性名中含有连字符或者空格），就要使用`'`或者`"`将属性名包裹，例如：

```javascript
var a = {
  user-name: 'Andy' // 报错，JavaScript 把属性名中的 - 当减号操作符处理
};

var a = {
  'user-name': 'Andy' // OK
};

var b = {
  user name: 'Andy' // 报错，JavaScript 没把 user name 当作一个整体
};

var b = {
  'user name': 'Andy' // OK
};

var c = {
  user_name: 'Andy' // OK 下划线是可以的
};
```

没有属性的对象是**空对象**，我们可以用如下方式声明一个空对象：

```javascript
var nullObject = {};
```

值得注意的是，属性值可以是表达式，如果我们在声明对象的时候用表达式做属性值，那么当我们访问到了该属性的时候，我们得到的就是表达式的返回值，例如：

```javascript
var a = {
  name: '陈' + '贝拉',
  age: 5 + 10 + 5,
  hobbies: ['旅行', '购物'].concat(['游泳', '睡觉']),
  married: !true
}

console.log(a); // {name: '陈贝拉', age: 20, hoobbies: ['旅行', '购物', '游泳', '睡觉'], married: false}
```
> 不仅是对象的属性，实际上数组的成员也可以是表达式，效果跟上面所说的一样。

## 对象和数组
对象和数组一样，都是复合类型的数据，它们都是由多种数据类型构成。在实际应用中，数组适合用来描述像列表一样的数据，比如菜单，名单等。而对象适合用来描述由多个属性构成的数据，比如，某个用户，某本书。

``` javascript
// 数组，用来表示像列表一样的数据
var bookList = ['双城记'， '瓦尔登湖', '红楼梦'， '西游记'];

// 对象，用来描述由多个属性构成的数据
var book = {
  title: '双城记',
  author: '狄更斯',
  years: 1859
};
```

数组的成员可以是任何类型的数据，同样的，对象的属性值也可以是**任何类型**的数据。也就是说，对象的属性值可以是数组，数组的成员可以是对象。

```javascript
// 成员是对象的数组
var bookList = [
  {
    title: '双城记',
    author: '查尔斯·狄更斯',
    years: 1859
  },
  {
    title: '瓦尔登湖',
    author: '亨利·戴维·梭罗',
    years: 1854
  },
  {
    title: '红楼梦',
    author: '曹雪芹',
    years: 1791
  },
  {
    title: '西游记',
    author: '吴承恩',
    years: 1592
  }
];

// 属性 hobbies 是数组的对象
var user = {
  name: '陈贝拉',
  hobbies: ['游泳', '划船', '攀岩']
};
```
当数组的成员是对象时，我们依然可以使用数组的方法来操作数组，实际上，不管数组的成员由什么类型的数据组成，我们都可以使用数组的方来来操作数组，例如：

```javascript
var a = [];

a.push({
  name: '王树',
  age: 20
});
console.log(a); // [{name: '王树', age: 20}]

var b = {
  title: '狂人日记',
  author: '鲁迅'
};
a.push(b);

console.log(a); // [{name: '王树', age: 20}, {title: '狂人日记', author: '鲁迅'}]

a.push('字符串');
console.log(a); // [{name: '王树', age: 20}, {title: '狂人日记', author: '鲁迅'}, '字符串']
```

既然对象的属性值可以是任何类型的数据，那么对象的属性值可以是对象。

``` javascript
var user = {
  name: '陈贝拉',
  hobbies: ['游泳', '划船', '攀岩'],
  occupation: { // 用对象描述的职业信息
    title: '健身教练', // 称谓
    salary: 8888 // 薪水
  }
}
```

## 对象属性的获取

与数组和字符串一样，我们可以通过成员操作符`[]`获取对象属性的属性值，但不同的是，数组和字符串通常是通过`[数字]`的形式获取，而对象的属性通常是通过`[字符串]`的形式获取，例如：

```javascript
// 字符串和数组通常情况下通过 [数字] 取到成员
var a = 'abcdefg';
console.log(a[0]); // 'a'
var menu = ['宫保鸡丁', '芹菜牛肉', '番茄鸡蛋', '车螺芥菜汤'];
console.log(menu[0]); // '宫保鸡丁'

// 对象通常情况下通过 [字符串] 取到成员
var user = {
  name: '陈贝拉',
  hobbies: ['游泳', '划船', '攀岩']
};
console.log(user['name']); // 陈贝拉
console.log(user['hobbies']); // ['游泳', '划船', '攀岩']
console.log(user['hobbies'][0]); // '游泳'

// 还可以是字符串类型的变量
var proto = 'name';
console.log(user[proto]); // 陈贝拉
```

对象的属性是对象的情况下，可以使用多个`[]`获取到信息，例如：

``` javascript
var user = {
  name: '陈贝拉',
  occupation: { // 用对象描述的职业信息
    title: '前端开发', // 称谓
    salary: 8888, // 薪水
    base: {
      city: '深圳',
      province: '广东',
      country: '中华人民共和国'
    }
  }
};

console.log(user['occupation']['title']); // '前端开发'
console.log(user['occupation']['base']['city']); // '深圳'
```
在对象里，除了成员操作符`[]`我们还可以通过一种另外一种的成员操作符`.`取到对象的属性值，同时`[]`和`.`操作符还能混用，因此上边的代码可以写成这样：

```javascript
var user = {
  name: '陈贝拉',
  occupation: { // 用对象描述的职业信息
    title: '前端开发', // 称谓
    salary: 8888, // 薪水
    base: {
      city: '深圳',
      province: '广东',
      country: '中华人民共和国'
    }
  }
};

console.log(user.occupation.title); // '前端开发'
console.log(user.occupation.base.city); // '深圳'

// . 和 [] 可以混合使用
console.log(user.occupation['base'].city); // '深圳'

```
> 到这里有人可能会有疑问，之前学字符串和数组的时候也碰到过`'123'.length`或者`[1,2,3].slice(0)`以及`[1,2,3].pop()`等等的使用了`.`的地方，实际上这些`.`就是上文提到的成员操作符，也可以使用`[]`代替，例如`'123'['length']`是合法的。
>
> 在 JavaScript 中，除了`null`和`undefined`外所有类型的数据都可以像对象一样通过成员操作符访问到其中的属性。
>
> 关于上面的知识点，往后会有更详细的说明。

通常情况下优先使用`.`操作符，因为简单，一个小点就能搞定。但是在属性名比较特殊（比如包含空格或者连字符）或者我们需要用变量做属性名的时候，使用`[]`，例如：

```javascript
var user = {
  'user-name': 'qwert@qwe.com',
  'nice name': 'Ciao',
  'password': '123456'
};
var proto = 'nice name';

console.log(user['user-name']); // 属性名特殊用 []
console.log(user[proto]); // 用变量做属性名使用 []，这里等同于 user['nice name']
console.log(user.password); // 直接一个小点能够搞定，就不需要用 []

// 如果不小心用错，JavaScript 会报错
console.log(user.user-name); // 报错，JavaScript 把 user-name 中的 - 当成了减号操作符
console.log(user.proto); // 取不到属性值，因为 JavaScript 把它看成了 user['proto'] ，而对象 user 里没有 proto 这个属性
console.log(user[password]); // 报错，没有定义 password 这个变量
console.log(user['password']); // 没毛病，就是多写了些字符
```

> 本书往后的示例代码会按照上面的约定使用`[]`和`.`。

当数组的成员是对象，对象的成员是数组的时候，我们依然可以按照`[]`和`.`的基本用法取到相关信息。

```javascript
// 成员是对象的数组
var bookList = [
  {
    title: '双城记',
    author: '查尔斯·狄更斯',
    years: 1859
  },
  {
    title: '瓦尔登湖',
    author: '亨利·戴维·梭罗',
    years: 1854
  },
  {
    title: '红楼梦',
    author: '曹雪芹',
    years: 1791
  },
  {
    title: '西游记',
    author: '吴承恩',
    years: 1592
  }
];
console.log(bookList[0]); // { title: '双城记', author: '查尔斯·狄更斯', years: 1859 }
console.log(bookList[0].title); // '双城记'


// 属性 hobbies 是数组的对象
var user = {
  name: '陈贝拉',
  hobbies: ['游泳', '划船', '攀岩']
};

console.log(user.hobbies); // ['游泳', '划船', '攀岩']
console.log(user.hobbies[1]); // '划船'
```

## 属性的添加和修改

我们可以通过成员操作符`[]`或者`.`给对象的属性赋值，例如：

```javascript
var user = {
  name: '陈贝拉',
  hobbies: ['游泳', '划船', '攀岩']
};

// 使用 . 给属性 name 赋值
console.log(user.name); // '陈贝拉'
user.name = '王二狗';
console.log(user.name); // '王二狗'

// 使用 [] 给属性 hobbies 赋值
console.log(user.hobbies); // ['游泳', '划船', '攀岩']
user['hobbies'] = ['喝酒', '撸串', '打游戏'];
console.log(user.hobbies); // ['喝酒', '撸串', '打游戏']


console.log(user); // {name: '王二狗', hobbies: ['喝酒', '撸串', '打游戏']}
```

同时我们也可以使用`[]`或者`.`给对象添加属性，例如：

```javascript
// 空对象，没有任何属性
var user = {};

// 使用 . 给对象 user 添加 name 属性
user.name = '董大妈';

// 使用 [] 给对象 user 添加 hobbies 属性
user['hobbies'] = ['说自己是董小姐'];

console.log(user); // {name: '董大妈', hobbies: ['说自己是董小姐']}
```

当我们通过`[]`或者`.`选中了对象中已经存在的属性，给其赋值的话，就是修改原有属性的值。而如果我们选中的是对象中没有的属性，给其赋值的时候，就是给对象添加该属性并且给属性赋值。

```javascript
var user = {
  name: '陈贝拉'
};

// 修改原有属性的值
user.name = '狗二蛋';

// 给对象 user 添加 hobbies 并赋值
user.hobbies = ['吃饭', '睡觉', '葛优躺'];

console.log(user); // {name: '狗二蛋', hobbies: ['吃饭'， '睡觉', '葛优躺']}
```

使用`delete`操作符，删除对象的属性，例如：

```javascript
var user = {
  name: '陈贝拉'
};
console.log(user); // {name: '陈贝拉'}

delete user.name;
console.log(user); // {}
```

## 对象练习
1. 根据下表声明一个名为`banana`的对象：
   <table>
    <thead>
     <tr>
      <td>属性名</td>
      <td>属性值</td>
     </tr>
    </thead>
    <tbody>
     <tr>
      <td>name</td>
      <td>'香蕉'</td>
     </tr>
     <tr>
      <td>colors</td>
      <td>['黄色', '绿色']</td>
     </tr>
     <tr>
      <td>price</td>
      <td>1.99</td>
     </tr>
     <tr>
      <td>sold-out</td>
      <td>true</td>
     </tr>
    </tbody>
   </table>
2. 根据下表声明一个名为`coconut`的对象：

   <table>
    <thead>
     <tr>
      <td>属性名</td>
      <td>属性值</td>
     </tr>
    </thead>
    <tbody>
     <tr>
      <td>name</td>
      <td>'椰子'</td>
     </tr>
     <tr>
      <td>colors</td>
      <td>['黄色', '棕色']</td>
     </tr>
     <tr>
      <td>sold-out</td>
      <td>false</td>
     </tr>
     <tr>
      <td>on-sale</td>
      <td>true</td>
     </tr>
     <tr>
      <td>off</td>
      <td>15</td>
     </tr>
     <tr>
      <td>price</td>
      <td>
        <table>
          <thead>
            <tr>
              <td>属性名</td>
              <td>属性值</td>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>large</td>
              <td>4.99</td>
            </tr>
            <tr>
              <td>medium</td>
              <td>3.99</td>
            </tr>
            <tr>
              <td>small</td>
              <td>2.99</td>
            </tr>
          </tbody>
        </table>
      </td>
     </tr>
    </tbody>
   </table>
3. 声明一个数组，成员是上面的两个对象。
4. 根据下面数组回答问题。
 
 ``` javascript
 var menu = [
      {
        name: '紫菜蛋花汤',
        price: 18,
        type: '汤'
      },
      {
        name: '爆炒牛河',
        price: 25,
        type: '小炒'
      },
      {
        name: '卤猪肚',
        price: 32,
        type: '卤菜'
      }
 ];
 ```
 
 * a. 获取`name`的值为`'卤猪肚'`的对象。
 * b. 将`name`的值为`'卤猪肚'`的对象的`price`属性的值改为`37`。
 * c. 获取`name`的值为`'爆炒牛河'`的对象的`price`属性的值。
 * d. 获取`name`的值为`'紫菜蛋花汤'`的对象的`type`属性的值改为`'清汤'`。
 * e. 在`menu`的末尾追加一个如下表所示的对象作为成员。
 
     <table>
      <thead>
       <tr>
        <td>属性名</td>
        <td>属性值</td>
       </tr>
      </thead>
      <tbody>
       <tr>
        <td>name</td>
        <td>'白灼时蔬'</td>
       </tr>
       <tr>
        <td>price</td>
        <td>19</td>
       </tr>
       <tr>
        <td>type</td>
        <td>'水煮'</td>
       </tr>
      </tbody>
     </table>
 
5. 根据下面数组回答问题。

 ```javascript
 var namelist = [
      {
        name: '陈贝拉',
        hobbies: ['唱歌', '二次元'],
        occupation: {
          title: '前端工程师',
          salary: 888
        }
      },
      {
        name: '李约翰',
        hobbies: ['健身', '足球', '古典乐'],
        occupation: {
          title: '测试工程师',
          salary: 999
        }
      },
      {
        name: '刘莉雯',
        hobbies: ['烹饪', '画画', '马拉松'],
        occupation: {
          title: 'UI设计师',
          salary: 777
        }
      }
 ]
 ```
 
 * a. 写出将`name`为`'陈贝拉'`的对象的`salary`改为`666`的代码。 
 * b. 写出将`name`为`'李约翰'`的对象的`hobbies`属性值前面追加一个成员`'威士忌'`的代码。 
 * c. 写出将`name`为`'刘莉雯'`的对象的`title`属性改为`'视觉设计师'`的代码。 
 * d. 写出给数组中每个成员的`occupation`属性增加一个`years`属性，它们的值依次是`1``1.5``2`的代码。 
 * e. 写出从数组中删除`name`为`'李约翰'`的对象的代码。 
 
6. 根据下表回答问题。

  <table>
    <thead>
     <tr>
      <td>属性名</td>
      <td>属性值</td>
     </tr>
    </thead>
    <tbody>
     <tr>
      <td>name</td>
      <td>'椰子'</td>
     </tr>
     <tr>
      <td>colors</td>
      <td>['黄色', '棕色']</td>
     </tr>
     <tr>
      <td>on-sale</td>
      <td>true</td>
     </tr>
     <tr>
      <td>price</td>
      <td>
        <table>
          <thead>
            <tr>
              <td>属性名</td>
              <td>属性值</td>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>large</td>
              <td>4.99</td>
            </tr>
            <tr>
              <td>medium</td>
              <td>3.99</td>
            </tr>
            <tr>
              <td>small</td>
              <td>2.99</td>
            </tr>
          </tbody>
        </table>
      </td>
     </tr>
    </tbody>
   </table>
   
   * a.现在有一个对象`var coconut = {}`用成员操作符给`coconut`赋值，让`coconut`可以描述上面的表格。
   * b.将 a 小题得到的对象中的`on-sale`属性删除。
   * c.将 b 小题得到的对象中`price`下的`small`属性删除。
