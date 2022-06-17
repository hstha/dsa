# Problem Solving Approach / Algorithms
- Use this approach only when you don't have an idea to solve the problem.

## What is algorithm?
- Algorithm is a set of steps to solve a problem.
- Why do we need to use algorithm?
  - Almost everything that you do in programming involves soke king of algorithms.
  - It's the foundation for being a successful problem solver and developer.
  - And most important it comes in interviews.

## How to improve in solving problems?
a. Devise a plan or strategies for solving problems.
- Understand the problem
- Explore concrete examples
- Break it down into steps
- Solve/Simplify
- Look back and refactor

b. Master common problem solving patterns.

### Problem Solving Approach
  a. Understand the problem
  - Can I restate the problem in my own words?
  - What are the inputs that go into the problem?
  - What are the outputs that should come from the solution to the problem?
  - Can the outputs be determined from the inputs? In other words, do I have enough information to solve the problem? If so, can I just solve the problem? If not, can I still solve the problem?
  - How should I label the important pieces of data in the problem?

    ```js
    // Example: Write a function which takes two numbers and returns their sum.
    /*
      1. Can I restate the problem in my own words?
        => implement addition of two numbers and return the result
      2. What are the inputs that go into the problem?
        => two integers
        => two floats
        => two decimals
        => combinations of above
        => what about large numbers?
        => what if string is placed instated of number?
      3. What are the outputs that should come from the solution to the problem?
        => what should the result be if two inputs are of different data types like int and floats, int and decimals, etc.
        => what if the inputs are very large numbers which programs won't support? Should the output show infinity or an error?
      4. Can the outputs be determined from the inputs? In other words, do I have enough information to solve the problem? If so, can I just solve the problem? If not, can I still solve the problem?
        => yes
      5. How should I label the important pieces of data in the problem?
        => function name, arguments names, return value data type
    */
    ```

  b. Explore concrete examples
  - Coming up with examples can help you understand the problem better.
  - Examples also provide sanity checks that your eventual solution works how it should.
  - While exploring examples:
    - Start with simple examples.
    - Progress to more complex examples.
    - Explore examples with empty or invalid inputs.
    
  ```js
  // Example: Write a function which takes two numbers and returns their sum.
  add(1, 2); // returns 3
  add(1, 2.5); // returns 3.5
  add(1, "2"); // returns throw invalid argument error
  add(1, "2.5"); // returns throw invalid argument error
  add("1", "2"); // returns throw invalid argument error
  add("qwe", "asd"); // throw invalid argument error
  add(); // throw no arguments error
  ```
  
  c. Break it down into steps
  - Explicitly write out the steps we need to take.

  ```js
  // Example: Write a function which takes two numbers and returns their sum.
  function add(a, b) {
    // throw error if no arguments are passed
    // throw error if arguments aren't integers or floats or decimals
    // add the two numbers and return the result
  }
  ```

  d. Solve/Simplify
  - Solve simpler problem if you can't solve complex problem out of the box.
  - After solve simpler problem than try solving complex problem.
    
  ```js
  // Example: Write a function which takes two numbers and returns their sum.
  // Simpler problem
  function add(a, b) {
    return a + b;
  }

  // Complex problem
  function add(a, b) {
    if (typeof a === "number" && typeof b === "number") {
      return a + b;
    } else {
      throw new Error("Invalid arguments");
    }
  }
  ```

  e. Look back and refactor
  - After you have completed the task, look back at your code and refactor it.
  - Ask following questions to refactor your code:
    - Can you check the result?
    - Can you derive the result differently?
    - Can you understand it at a glance?
    - Can you use the result or method for some other problem?
    - Can you improve the performance of your solution?
    - Can you think of other ways to refactor?
    - How have other people solved this problem?

  ```js
  // Example: Write a function which takes two numbers and returns their sum.

  /*
  * Added two number
  * @param {number} a - first number
  * @param {number} b - second number
  * @return {number} - sum of two numbers
  */
  add(a, b) {
    if(typeof a !== "number" && typeof b !== "number") {
      throw new Error("Invalid arguments");
    }

    return a + b;
  }
  ```

### Problem Solving Patterns
a. Frequency Counter
- Frequency Counter is a data structure that stores a list of items and their frequency.
- This can often avoid the need for nested loops or O(n^2) operations with arrays / strings.
- This approach is useful when you have multiple pieces of data or inputs and you need to compare them to see if they 
  - consists of similar values
  - are anagram of one another
  - contained in one another

```js
/*
* Gets the frequency of each element in the array
* @param {array} arr - Array of elements
* @return {object} - Object with key as element and value as frequency
*/
function getFrequency(arr) {
  const frequency = {};
  for(let val of arr) {
    frequency[val] = (frequency[val] || 0) + 1;
  }
  
  return frequency;
}
```

```js
// Example: Write a function called same, which accepts two arrays. THe function should return true if every value in the array has its corresponding value squared in the second array. The frequency of values must be the same.
// same([1, 2, 3], [4, 1, 9]); // true
// same([1, 2, 3], [1, 9]); // false
// same([1, 2, 1], [4, 4, 1]); // false

/*
* Check if values in one array are squared in the other array
* @param {array} arr1 - First array
* @param {array} arr2 - Second array
* @return {boolean} - True if values in one array are squared in the other array, false otherwise
*/
function same(arr1, arr2) {
  if (arr1.length !== arr2.length) {
    return false;
  }

  const frequencyCounter1 = getFrequency(arr1);
  const frequencyCounter2 = getFrequency(arr2);

  for (let key in frequencyCounter1) {
    if (!(key ** 2 in frequencyCounter2)) {
      return false;
    }

    if (frequencyCounter2[key ** 2] !== frequencyCounter1[key]) {
      return false;
    }
  }

  return true;
}

console.log(same([1, 2, 3], [4, 1, 9])); // true
console.log(same([1, 2, 3], [1, 9])); // false
console.log(same([1, 2, 1], [4, 4, 1])); // false
```

```js
// Example: Given two strings, write a function to determine if the second string is an anagram of the first.
// An anagram is a word, phrase, or name formed by rearranging the letters of another, such as cinema, formed from iceman.

// isAnagram('', ''); // true
// isAnagram('aaz', 'zza'); // false
// isAnagram('anagram', 'nagaram'); // true
// isAnagram('rat', 'car'); // false
// isAnagram('awesome', 'awesome'); // true
// isAnagram('qwerty', 'awesom'); // false
// isAnagram('texttwisttime', 'timetwisttext'); // true
// isAnagram('cinema', 'iceman'); // true

/*
* Check if two strings are anagrams of one another
* @param {string} str1 - First string
* @param {string} str2 - Second string
* @return {boolean} - True if two strings are anagrams of one another, false otherwise
*/
function isAnagram(str1, str2) {
  if (str1.length !== str2.length) {
    return false;
  }

  const frequencyCounter1 = getFrequency(str1);
  const frequencyCounter2 = getFrequency(str2);

  for (let key in frequencyCounter1) {
    if (!(key in frequencyCounter2)) {
      return false;
    }

    if (frequencyCounter2[key] !== frequencyCounter1[key]) {
      return false;
    }
  }

  return true;
}

console.log(isAnagram('', '')); // true
console.log(isAnagram('aaz', 'zza')); // false
console.log(isAnagram('anagram', 'nagaram')); // true
console.log(isAnagram('rat', 'car')); // false
console.log(isAnagram('awesome', 'awesome')); // true
console.log(isAnagram('qwerty', 'awesom')); // false
console.log(isAnagram('texttwisttime', 'timetwisttext')); // true
console.log(isAnagram('cinema', 'iceman')); // true
```

b. Multiple Pointers
- Creating pointers or values that correspond to an index or position and move towards the beginning, end or middle based on a certain condition.
- Very efficient for solving problems with minimal space complexity as well.

```js
// Example: Write a function called sumZero which accepts a sorted array of integers. The function should find the first pair of numbers that sum to 0. Return an array that includes both values that sum to zero or undefined if a pair does not exist.

// sumZero([-3, -2, -1, 0, 1, 2, 3]) // [-3, 3]
// sumZero([-2, 0, 1, 3]) // undefined
// sumZero([1, 2, 3]) // undefined

/*
* Finds the first pair of numbers that sum to 0
* @param {array} arr - Array of integers
* @return {array} - Array of two integers that sum to 0
*/
function sumZero(arr) {
  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    let sum = arr[left] + arr[right];
    if (sum === 0) {
      return [arr[left], arr[right]];
    } else if (sum > 0) {
      right--;
    } else {
      left++;
    }
  }

  return undefined;
}

console.log(sumZero([-3, -2, -1, 0, 1, 2, 3])); // [-3, 3]
console.log(sumZero([-2, 0, 1, 3])); // undefined
console.log(sumZero([1, 2, 3])); // undefined
```

```js
// Example: Implement a function called countUniqueValues, which accepts a sorted array, and counts the unique values in the array. There can be negative numbers in the array, but it will always be sorted.

// countUniqueValues([1, 1, 1, 1, 1, 2]) // 2
// countUniqueValues([1, 2, 3, 4, 4, 4, 7, 7, 12, 12, 13]) // 7
// countUniqueValues([]) // 0
// countUniqueValues([-2, -1, -1, 0, 1]) // 4

/*
* Counts the unique values in the array
* @param {array} arr - Array of integers
* @return {number} - Number of unique values in the array
*/
function countUniqueValues(arr) {
  let i = 0;
  let j = 1;

  while (j < arr.length) {
    if (arr[i] !== arr[j]) {
      i++;
      arr[i] = arr[j];
    }
    j++;
  }

  return i + 1;
}

console.log(countUniqueValues([1, 1, 1, 1, 1, 2])); // 2
console.log(countUniqueValues([1, 2, 3, 4, 4, 4, 7, 7, 12, 12, 13])); // 7
console.log(countUniqueValues([])); // 0
```

c. Sliding Window
- This pattern involves creating a window which can either be an array or number from one position to another.
- Depending on a certain condition, the window either increases or closes (and a new new window is created).
- Very useful for keeping track of a subset of data in an array, string etc.
- This approach is useful in keeping track of a subset of data in larger set of data.

```js
// Example: Write a function called maxSubarraySum which accepts an array of integers and a number called n. The function should calculate the maximum sum of n consecutive elements in the array.

// maxSubarraySum([1, 2, 5, 2, 8, 1, 5], 2) // 10
// maxSubarraySum([1, 2, 5, 2, 8, 1, 5], 4) // 17
// maxSubarraySum([4, 2, 1, 6], 1) // 6
// maxSubarraySum([4, 2, 1, 6, 2], 4) // 13
// maxSubarraySum([], 4) // null

/*
* Finds the maximum sum of n consecutive elements in the array
* @param {array} arr - Array of integers
* @param {number} n - Number of consecutive elements to sum
* @return {number} - Maximum sum of n consecutive elements in the array
*/
function maxSubarraySum(arr, num) {
  let maxSum = 0;
  let tempSum = 0;

  if(arr.length < num) {
    return null;
  }
  
  for(let i = 0; i < num; i++) {
    maxSum += arr[i];
  }

  tempSum = maxSum;
  
  for(let i = num; i < arr.length; i++) {
    tempSum = tempSum - arr[i - num] + arr[i];
    maxSum = Math.max(maxSum, tempSum);
  }

  return maxSum;
}

console.log(maxSubarraySum([1, 2, 5, 2, 8, 1, 5], 2)); // 10
console.log(maxSubarraySum([1, 2, 5, 2, 8, 1, 5], 4)); // 17
console.log(maxSubarraySum([4, 2, 1, 6], 1)); // 6
console.log(maxSubarraySum([4, 2, 1, 6, 2], 4)); // 13
console.log(maxSubarraySum([], 4)); // null
```

d. Divide and Conquer
- This pattern involves dividing the problem into smaller chunks and then solving those chunks recursively.
- This pattern can tremendously decrease time complexity.

```js
// Example: Given a sorted array of integers, write a function called search, that accepts a value and returns the index where the value passed to the function is located. If the value is not found, return -1.

// search([1, 3, 5, 7], 8) // -1
// search([1, 3, 5, 7], 3) // 1
// search([1, 3, 5, 7], 5) // 2

function search(arr, val) {
  let min = 0;
  let max = arr.length - 1;

  while (min <= max) {
    let mid = Math.floor((min + max) / 2);
    if (arr[mid] === val) {
      return mid;
    } else if (arr[mid] < val) {
      min = mid + 1;
    } else {
      max = mid - 1;
    }
  }

  return -1;
}
```

e. Many more!
