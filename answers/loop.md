## 循环语句答案

1.  如下

    ```javascript
    // a
    var nums = [2, 4, 6, 8, -9];
    var i = 0;
    while(i < nums.length){
      nums[i] = nums[i] * 2;
      i++;
    }
    console.log(nums);
    
    // b
    var nums = [2, 4, 6, 8, -9];
    var i = 0;
    do {
      nums[i] = nums[i] * 2;
      i++;
    } while(i < nums.length);
    console.log(nums);
    
    // c
    var nums = [2, 4, 6, 8, -9];
    for(var i = 0 ; i < nums.length ; i++){
      nums[i] = nums[i] * 2;
    }
    console.log(nums);
    ```

2. 如下

    ```javascript
    var n = 12, m = 28;
    var t;
    
    while (m !== 0) {
      t = m;
      m = n % m;
      n = t;
    }
    console.log(n);
    ```

3. 如下

    ```javascript
    var n = 12, m = 28;
    var a = n, b = m;
    var t;
    
    while (b !== 0) {
      t = b;
      b = a % b;
      a = t;
    }
    
    n = n / a;
    m = m / a;
    
    console.log(n, m);
    ```
    
4. 如下

    ```javascript
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
5. 如下

    ```javascript
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
6. 如下

    ```javascript
    var nums = ['Jognny', 'Lorin', 'Quadro', 'Hank', 'Collin', 'Roberta'];
    var result = [];
    for(var i = 0; i < nums.length; i++) {
      if (nums[i].length >= 4 && nums[i].length <= 6) {
        result.push(nums[i]);
      }
    }
    console.log(result);
    ```
7. 如下

    ```javascript
    var user = {
      name: 'Bella',
      age: 28,
      gender: 'female'
    };
    var result = {};
    for (var key in user) {
      result[user[key]] = key;
    }
    console.log(result);
    ```
8. 如下

    ```javascript
    var gradeOne = {
      classOne: ['语蕊', '杨文丽', '耿雨真', '能宏达', '介山槐'],
      classTwo: ['暨嘉运', '白秋', '永黛娥', '廖俊风'],
      classThree: ['苌晶滢', '夏菡', '慕容天青', '释鸿文', '隋乐咏', '衣月桂', '闫雨华']
    };
    
    
    // a
    var maxKey = 'classOne', maxValue = gradeOne[maxKey];
    for (var key in gradeOne) {
      if (maxValue.length < gradeOne[key].length) {
        maxValue = gradeOne[key];
        maxKey = key;
      }
    }
    console.log(maxKey, maxValue);
    
    //  b
    var klass = '', number = 0;
    for (var key in gradeOne) {
      if ( gradeOne[key].indexOf('白秋') !== -1) {
        number = gradeOne[key].indexOf('白秋');
        klass = key;
      }
    }
    console.log(klass, number);
    
    //  c
    for (var key in gradeOne) {
      var index = gradeOne[key].indexOf('慕容天青');
      if (index !== -1) {
        gradeOne[key].splice(index, 1);
        break;
      }
    }
    console.log(gradeOne);
    ```