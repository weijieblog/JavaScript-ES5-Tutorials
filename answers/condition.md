## 条件语句练习答案

1. 

 * `a`的值为`2`
 * `b`的值为`5`
 * `c`的值为`0`
 * `d`的值为`20`
 * `e`的值为`5`

2. 

 * `a`的值为`2`
 * `b`的值为`5`
 * `c`的值为`4`
 * `d`的值为`7`
 * `e`的值为`5`
 * `f`的值为`5`

3. 一个对象，四个代码块
4. `{} + 1`中的`{}`是代码块，`1 + {}`中的`{}`是对象，所以不等。
5. `#2`、`#12`被运行了
6. `#1`、`#2`、`#3`、`#8`、`#9`、`#10`被运行了
7. 

 * `#1`：`'你好'`
 * `#2`：`'祝你工作顺利'`
 * `#3`：`'你好个毛`、`'祝你工作顺利'`

8. 

 * (a)：如下代码
 
    ```javascript
    if(user.gender === 'male') {
      greeting = '先生，你好';
    } else if (user.gender === 'female') {
      greeting = '女士，你好';
    }
    ```
 * (b)：如下代码

    ```javascript
    switch(user.gender) {
      case 'male':
        greeting = '先生，你好';
        break;
      case 'female':
        greeting = '女士，你好';
        break;       
    }
    ```

9. 如下代码

    ```javascript
    var num1 = 23,
        num2 = 888,
        num3 = 2;
    var result = [];
    
    var min = num1, 
        nom = num2, 
        max = num3, 
        temp;
    
    
    if (min > nom) {
      temp = min;
      min = nom;
      nom = temp;
    }
    
    if (min > max) {
      temp = min;
      min = max;
      max = temp;
    }
    
    if (nom > max) {
      temp = nom;
      nom = max;
      max = temp;
    }
    
    result.push(min, nom, max);
    ```

10. 将上边代码的`result.push(min, nom, max)`换成`result.push(max, nom, min)` 即可。

11. 

 * (a)：如下代码
 
    ```javascript
    if(spending < 10000) {
      level = 'VIP';
    } else if (spending >= 10000 && spending <= 30000) {
      level = '黄金 VIP';
    }else if (spending > 30000) {
      level = '钻石 VIP';
    }
    ```
 * (b)：如下代码

    ```javascript
    switch(true) {
      case spending < 10000:
        level = 'VIP';
        break;
      case spending >= 10000 && spending <= 30000:
        level = '黄金 VIP';
        break;
      case spending > 30000:
        level = '钻石 VIP';
        break;
    }
    ```
    
12. 如下代码    

    ```javascript
    if (num % 2 === 1) {
      result = 'odd';
    } else {
      result = 'even'
    }
    ```