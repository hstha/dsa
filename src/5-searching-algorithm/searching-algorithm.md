# Searching Algorithm
- Searching is the process of finding a specific item in a collection.
- Type of searching algorithms:
  - Linear Search
    - Linear search is a search algorithm that searches sequentially through the collection.
    ```js
    // Example: Write a function that accepts an array and a value and returns the index at which the value exists else -1.

    // Solution 1
    /*
    * Check if the array has the given value.
    * @param {array} arr - The array to be searched.
    * @param {number} value - The value to be searched for.
    * @return {number} - The index at which the value exists else -1.
    */
    function linearSearch(arr, value) {
      for(let i = 0; i < arr.length - 1; i++) {
        if(arr[i] === value) {
          return i;
        }
      }

      return -1;
    }

    // Solution 2
    /*
    * Check if the array has the given value.
    * @param {array} arr - The array to be searched.
    * @param {number} value - The value to be searched for.
    * @return {number} - The index at which the value exists else -1.
    */
    function linearSearch(arr, value) {
      return arr.indexOf(value);
    }
    ```

    - In js, Array.indexOf, Array.find, Array.findIndex perform linear search under the hood.
    - O(n)
      - Linear search is O(n) time complexity.
      - Linear search is O(1) space complexity.
    - When to use:
     - When you know the collection is small and you want to find a specific item in it.

    - When not to use:
      - Linear search is not efficient for large collections.
      - Linear search is not efficient for collections that are sorted.

  - Binary Search
    - Binary search is a search algorithm that searches sequentially through the collection similar to linear search.
    - Binary search is a much faster from of search because rather than eliminating one element at a time you can eliminate half of the remaining elements at a time.
    - Binary search only works on sorted list of data.
    - The idea behind binary search is to divide the list into two halves and then search the half that contains the item you are looking for. If the item is not found, then you can search the other half. This process is repeated until you find the item or until you reach the end of the list.
    - Divide and conquer is used in binary search.

    ```js
    // Example: Write a function that accepts an array and a value and returns the index at which the value exists else -1.

    // Solution 1
    /*
    * Check if the array has the given value.
    * @param {array} arr - The array to be searched.
    * @param {number} value - The value to be searched for.
    * @return {number} - The index at which the value exists else -1.
    */
    function binarySearch(arr, value) {
      let left = 0;
      let middle = Math.floor(arr.length);
      let right = arr.length - 1;

      if(arr[middle] === value) {
        return middle;
      }

      if(value > arr[middle]) {
        return binarySearch(arr.slice(middle, right), value);
      }

      if(value < arr[middle]) {
        return binarySearch(arr.slice(left, middle), value);
      }

      return -1;
    }

    // Solution 2
    /*
    * Check if the array has the given value.
    * @param {array} arr - The array to be searched.
    * @param {number} value - The value to be searched for.
    * @return {number} - The index at which the value exists else -1.
    */
    function binarySearch(arr, length) {
      let start = 0;
      let end = arr.length - 1;
      let middle = Math.floor((start + end) / 2);

      while(arr[middle] !== value && start <= end) {
        if(value < arr[middle]) {
          end = middle - 1;
        } else {
          start = middle + 1;
        }

        middle = Math.floor((start + end) / 2);
      }

      return arr[middle] === value ? middle : -1;
    }
    ```

    - O(n)
      - Binary search is O(log n) time complexity.
      - Binary search is O(1) space complexity.
    - When to use:
      - If we have sorted collection of data.
    - When not to use:
      - If we have unsorted collection of data.
  
  - String search:
    - String search is a search algorithm that searches a sub string within a string.
    ```js
    // Example: Write a function that accepts a parent string and sub string and returns the frequency of the occupance of sub string in that parent string

    // Solution 1
    /*
    * Check the frequency of the sub string present in the parent string.
    * @param {string} parent - The parent string to be searched.
    * @param {string} sub - The sub string to be searched for.
    * @return {number} - The frequency of the occupance of sub string in that parent string.
    */
    function naiveStringSearch(parentStr, subStr) {
      let count = 0;
      let tempCount = 0;

      for(let i = 0; i < parentStr.length - subStr.length; i++) {
        if(parentStr[i] === subStr[0]) {
          for(let j = 0; j < subStr.length - 1; j++) {
            if(parentStr[i + j] !== subStr[j]) {
              break;
            } else {
              tempCount++;
            }
          }

          if(tempCount === subStr.length) {
            count++;
          }

          tempCount = 0;
        }
      }

      return count;
    }

    // Solution 2
    /*
    * Check the frequency of the sub string present in the parent string.
    * @param {string} parent - The parent string to be searched.
    * @param {string} sub - The sub string to be searched for.
    * @return {number} - The frequency of the occupance of sub string in that parent string.
    */
    function naiveStringSearch(parentStr, subStr) {
      let count = 0;
      for(let i = 0; i < parentStr.length; i++) {
        for(let j = 0; j < subStr.length; j++) {
          if(parentStr[i + j] !== subStr[j]) {
            break;
          } else if(j === subStr.length - 1) {
            count++;
          }
        }
      }

      return count;
    }
    ```