## 循环语句答案


```javascript
// 第四题
var nums = [2, 55, 1, 355, 2, 6, 8, 33, 65, 78];
var even = [], odd = [];
for(var i = 0; i < nums.length; i++) {
  if (nums[i] % 2 === 1) {
    odd.push(nums[i]);
  } else {
    even.push(nums[i]);
  }
}
console.log(even, odd); // [2, 2, 6, 8, 78] [55, 1, 255, 33, 65]
```

```javascript
// 第五题
var nums = ['Jognny', 'Lorin', 'Quadro', 'Hank', 'Collin', 'Roberta'];
var theShortest = nums[0], theLongest = nums[0];
for(var i = 1; i < nums.length; i++) {
  if (theShortest.length > nums[i].length) {
    theShortest = nums[i];
  }

  if (theLongest.length < nums[i].length) {
    theLongest = nums[i];
  }
}
console.log(theShortest, theLongest);
```


```javascript
// 第六题
var nums = ['Jognny', 'Lorin', 'Quadro', 'Hank', 'Collin', 'Roberta'];
var result = [];
for(var i = 0; i < nums.length; i++) {
  if (nums[i].length >= 4 && nums[i].length <= 6) {
    result.push(nums[i]);
  }
}
console.log(result);
```