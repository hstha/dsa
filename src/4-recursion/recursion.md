# Recursion
- Recursion is a process that calls itself with different input until certain condition is met.
- Before learning about recursion, we need to know about call stacks.
  - In almost all programming languages, there is a build in data structure that manages what happens when functions are invoked which is called call stack.
  - Any time a function is invoked it is placed (pushed) on the top of the call stack.
  - When the function returns, it is removed (popped) from the top of the call stack.

  ```js
  // Example of call stack
  function takeShower() {
    return 'Showering!';
  }

  function cookFood() {
    let items = ["Oatmeal", "Eggs", "Protein Shake"];

    return items[Math.floor(Math.random() * items.length)];
  }

  function eatBreakfast() {
    let meal = cookFood();

    return `Eating ${meal}!`;
  }

  function wakeUp() {
    takeShower();
    eatBreakfast();

    console.log("Ok ready to go to work!");
  }

  wakeUp();

  /*
  Step 1: When wakeUp is executing,
  callStack = [wakeUp];

  Step 2: When takeShower is executing inside wakeUp,
  callStack = [takeShower, wakeUp];

  Step 3: Since there is no another function to execute inside takeShower, so after takeShower is executed,
  callStack = [wakeUp];

  Step 4: When eatBreakfast is executing inside wakeUp,
  callStack = [eatBreakfast, wakeUp];

  Step 5: When cookFood is executing inside eatBreakfast,
  callStack = [cookFood, eatBreakfast, wakeUp];

  Step 6: When cookFood is executed,
  callStack = [eatBreakfast, wakeUp];

  Step 7: When eatBreakfast is executed,
  callStack = [wakeUp];

  Step 8: When wakeUp is executed,
  callStack = [];
  */
  ```

  - Why do we care about call stacks in recursion?
    - When we write recursive functions, we keep calling the same function over and over again until certain conditions are met. So function are continuously pushed inside the called stack and popped out when they return. For this reason we need to know about how the call stacks work.
- There are two important parts of a recursive function:
  - Base condition is the special condition that is used to stop the recursion.
  - Different Input is the input that is used to call the function again.

```js
// Example 1:

/*
* Counts down from a given number to 0.
* @param {number} num - The number to count down from.
*/
function countDown(num) {
  if (num <= 0) {
    console.log("All done!");
    return;
  }

  console.log(num);
  num--;
  countDown(num);
}

/*
Here, 
num <= 0 is the base condition.
num-- is the input that changes on each function call.
*/
```

```js
// Example 2:
/*
* Sum of all the range value form given number to 1
* @param {number} num - The number to start the sum from.
* @return {number} - The sum of all the range value form num to 1.
*/
function sumRange(num) {
  if (num === 1) {
    return 1;
  }

  return num + sumRange(num - 1);
}
```

```js
// Example 3:

/*
* Factorial of a given number
* @param {number} num - The number to calculate the factorial of.
* @return {number} - The factorial of the given number.
*/
function factorial(num) {
  if (num === 1) {
    return 1;
  }

  return num * factorial(num - 1);
}
```

- What are the pitfalls when writing a recursive function?
  - No base case
  - Forgetting to return or returning the wrong value

## Design pattern for recursion
- Helper Method Recursion
  - A helper method is a function that is called inside another function.
  - This is a design pattern that is used to make a function more readable.
  - This is done when we need to compile a list of data instead of tabulating one value over and over again.
  
  ```js
  // Syntax for helper method recursion

  function outerFunction(input) {
    let result = [];

    function helperFunction(helperInput) {
      // Modify the result variable
      helperFunction(helperInput--);
    }

    helperFunction(input);

    return result;
  }
  ```

  ```js
  // Collect all the odd values in an array

  /*
  * Collects all the odd values in an array
  * @param {array} arr - List of number that needs to be checked
  * @return {array} - List of odd values
  */
  function collectOddValues(arr) {
    let result = [];

    /*
    * The helper function that stores, the first index value of an array if it is odd.
    * @param {array} helperInput - List of numbers that needs to be checked
    * @return {undefined}
    */
    function getOddValue(helperInput) {
      if (helperInput.length === 0) {
        return;
      }

      if (helperInput[0] % 2 !== 0) {
        result.push(helperInput[0]);
      }

      getOddValue(helperInput.slice(1));
    }

    getOddValue(arr);

    return result;
  }
  ```

  - Pure Recursion
    - A pure recursive function is a function that calls itself without any external input.
    - A little hard to wrap your head around.

    ```js
    // Example of pure recursion

    /*
    * Collects all the odd values in an array
    * @param {array} arr - List of number that needs to be checked
    * @return {array} - List of odd values
    */
    function collectOddValues(arr) {
      let newArr = [];

      if(arr.length === 0) {
        return newArr;
      }

      if(arr[0] % 2 !== 0) {
        newArr.push(arr[0]);
      }

      newArr = newArr.concat(collectOddValues(arr.slice(1)));

      return newArr;
    }
    ```