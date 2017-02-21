## 数组练习答案

1. `var a = ['鸡蛋', '肉类', '果汁', '麦片', '牛奶'];` 
2. `var a = [3, 1, 4, 1, 5];` 
3. 
 - a. `3`
 - b. `collection[1] = '茑萝行';`
 - c. `collection[2];`
 - d. `collection.length;`
4. 
 - a. `1`
 - b. `menu[1] = '烤鸡';`
 - c. `menu[menu.length - 1];`
 - d. `menu[menu.length - 1] = '甜筒';`
5. 
 - a. `fruits.indexOf('香蕉');`
 - b. 如下代码
 
   ```javascript
   // 第一个'苹果'的索引
   var index = fruits.indexOf('苹果');
   
   // 第二个'苹果'的索引
   var result = fruits.indexOf('苹果', index + 1);
   ```
 - c. 同上

6. 
 - a. `numbers.indexOf(66546);`
 - b. 如下代码
 
   ```javascript
   // 第一个'苹果'的索引
   var index = numbers.indexOf(32);
   
   // 第二个'苹果'的索引
   index = numbers.indexOf(32, index + 1);
   
   // 第三个'苹果'的索引
   var result = numbers.indexOf(32, index + 1);
   ```
 - c. 同上
7. 
 - a. `namelist.splice(2, 1);`
 - b. `namelist.splice(1, 3);`
 - c. `namelist.splice(1, 0, 'Lily', 'Bella');`
 - d. `namelist.splice(3, 3, 'Lily', 'Bella');`

8. 
 - a. `codes.splice(1, 1);`
 - b. `codes.splice(1, 3);`
 - c. `codes.splice(codes.length, 0, 3, 5);`
 - d. `codes.splice(4, 5, 6);`

9. 
 - a. `['Saturday']`
 - b. `['Saturday', 'Sunday']`
 - c. `2`
 - d. `'Sunday'`
 - e. `['Saturday']`
10. 
 - a. `['Tuesday']`
 - b. `['Monday', 'Tuesday']`
 - c. `2`
 - d. `'Monday'`
 - e. `['Tuesday']`
11. 
 - a. 如下
 
 ```javascript
 one.push('Friday');
 one.unshift('Monday');
 ```
 - b. 如下
 
 ```javascript
 two.pop();
 two.shift();
 ```
 
 - c. 如下
 
 ```javascript
 two.pop();
 two.shift();
 
 two.unshift('Tuesday', 'Monday', 'Sunday');
 two.push('Thursday', 'Friday', 'Saturday');
 ```
 
12. 
 - a. `a.concat(a);`
 - b. `a.concat(b.concat(c));`
 - c. `[1, 2]`

13. 
 - a. `['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']`
 - b. `days.slice(2, 5);`
 - c. `days.slice(days.length - 2, days.length);`

14. 
 - a. 如下
 
 ``` javascript
 var a = [
   [1, 2, 3],
   [2, 2, 3],
   [3, 2, 3],
   [4, 2, 3]
 ];
 ```
 
 - b. 如下
 
 ```javascript
 a[1][0] = 1;
 a[2][0] = 1;
 a[3][0] = 1;
 ```
 
 - c. `a.pop();`

15. 

 - a. 如下
 
 ``` javascript
 var a = [
   [1, 2, 3],
   [4, 5, 6]
 ];
 ```
 - b. `a.push([7, 8, 9]);`
 - c. 如下
 
 ``` javascript
 a[0][1] = 0;
 a[1][1] = 0;
 a[2][1] = 0;
 ```