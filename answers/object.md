## 对象练习参考答案

1. 如下代码

  ```javascript
  var banana = {
      name: '香蕉',
      colors: ['黄色', '绿色'],
      price: 1.99,
      'sold-out': true
  };
  ```
2. 如下代码

  ```javascript
  var coconut = {
      name: '椰子',
      colors: ['黄色', '棕色'],
      'sold-out': false,
      'on-sale': true,
      off: 15,
      price: {
          large: 4.99,
          medium: 3.99,
          small: 2.99
      }
  }
  ```
  
3. `var fruits = [banana, coconut];`
4. a. `menu[2];`
   b. `menu[2].price = 37;`
   c. `menu[1].price;`
   d. `menu[0].type = '清汤';`
   e. `menu.push({name: '白灼时蔬', price: 19, type: '水煮'});`
5. a. `namelist[0].occupation.salary = 666;`
   b. `namelist[1].hobbies.unshift('威士忌');`
   c. `namelist[2].occupation.title = '视觉设计师';`
   d. 如下代码
   
   ```javascript
   namelist[0].occupation.years = 1;
   namelist[1].occupation.years = 1.5;
   namelist[2].occupation.years = 2;
   ```
   e. `namelist.splice(1, 1);`
6. a. 如下代码
   
   ```javascript
   var coconut = {};
   coconut.name = '椰子';
   coconut.colors = ['黄色', '棕色'];
   coconut['on-sale'] = true;
   coconut.price = {
       large: 4.99,
       medium: 3.99,
       small: 2.99
   }  
   ```
   b. `delete coconut['on-sale'];`
   c. `delete coconut.price.small;`