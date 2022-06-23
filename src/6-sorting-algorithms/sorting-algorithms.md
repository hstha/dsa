# Sorting Algorithms
- Sorting is the process of rearranging the elements of a collection so that they are in some order.
```
Example:
- Sorting numbers from smallest to largest.
- Sorting string alphabetically.
- Sorting movies based on release year.
- Sorting movies based on revenue.
```

## Why do we need to learn sorting algorithms?
- Sorting is an incredibly common task, so it's good to know how it works.
- THere are many different ways to sort things, and different techniques have their own advantages and disadvantages.

## Type of Sorting Algorithms
- Bubble Sort [Simple Sorting Algorithm]
- Selection Sort [Simple Sorting Algorithm]
- Insertion Sort [Simple Sorting Algorithm]
- Merge Sort [Intermediate Sorting Algorithm]
- Quick Sort [Intermediate Sorting Algorithm]
- Heap Sort [Intermediate Sorting Algorithm]
- Radix Sort [Intermediate Sorting Algorithm]

### Bubble Sort
- Bubble sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in wrong order.
- In this algorithm, the largest element is moved to the end of the collection.
- Steps:
  1. Loop through the collection from end to beginning, i from collection.length to 0. 
  2. Create an inner loop from beginning until one less than outer loop, j from 0 to i - 1.
  3. If the element at index j is greater than the element at index j + 1, swap them.
  4. Repeat steps 2 and 3 until the inner loop is complete.
  5. Repeat steps 1 and 2 until the outer loop is complete.
  6. Return the collection which is in sorted form.

  ```js
  // Syntax
  function swap(arr, i, j) {
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }

  // Solution 1: Without optimization
  function bubbleSort(collection) {
    for (let i = collection.length; i > 0; i--) {
      for (let j = 0; j < i - 1; j++) {
        if (collection[j] > collection[j + 1]) {
          swap(collection, j, j + 1);
        }
      }
    }
  }

  // Solution 2: With some optimization
  function bubbleSort(collection) {
    let hasSwapped = false;
    for (let i = collection.length; i > 0; i--) {
      hasSwapped = false;
      for (let j = 0; j < i - 1; j++) {
        if (collection[j] > collection[j + 1]) {
          swap(collection, j, j + 1);
          hasSwapped = true;
        }
      }

      if(!hasSwapped) {
        break;
      }
    }
  }
  ```
- O(n):
  - Time complexity is O(n^2) because of the nested loops.
  - Space complexity is O(1) because no additional space is used.

- When to use:
- When not to use:

### Selection Sort
- Selection sort is a simple sorting algorithm that works by selecting the small values into sorted position.
- In this algorithm, the smallest element is moved to the beginning of the collection.
- Steps:
  1. Store the first element as the smallest value we have seen so far.
  2. Compare this item to the next element in the collection until we find a smaller number.
  3. If a smaller number is found, store that element as smallest element and continue until the end of the array.
  4. If the smallest element is not the value (index) we initially began with, swap the two values.
  5. Repeat this with the next element until the collection is sorted.

  ```js
  // Syntax
  
  function swap(arr, i, j) {
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }

  function selectionSort(collection) {
    for (let i = 0; i < collection.length; i++) {
      let minIndex = i;
      for (let j = i + 1; j < collection.length; j++) {
        if (collection[j] < collection[minIndex]) {
          minIndex = j;
        }
      }

      if (minIndex !== i) {
        swap(collection, i, minIndex);
      }
    }
  }
  ```
- It swaps less than that of bubble sort, Why?
- O(n):
  - Time complexity is O(n^2) because of the nested loops.
  - Space complexity is O(1) because no additional space is used.
- When to use:
- When not to use:

### Insertion Sort
- Similar to bubble and selection sort.
- It builds up the sort by gradually creating a larger left portion which is always sorted.
- Steps:
  1. Start by picking the second element in the array.
  2. Now compare the second element with the one before it and swap if necessary.
  3. Continue to the next element and if it is in the incorrect order, iterate through the sorted portion (i.e. the left side) to place the element in the correct place.
  4. Repeat until the array is sorted.

  ```js
  // Syntax

  function insert(arr, removedValueIndex, insertValueIndex) {
    const removedValue = arr.splice(removedValueIndex, 1);
    arr.splice(insertValue, 0, removedValue);
  }

  function insertionSort(collection) {
    let insertIndex = -1;
    for(let i = 0; i < collection.length - 1; i++) {
      insertIndex = -1;
      for(let j = i; j >= 0; j--) {
        if(collection[i + 1] >= collection[j]) {
          break;
        }
        insertIndex = j;
      }

      if(insertIndex !== -1) {
        insert(collection, i + 1, insertIndex);
      }
    }
  }
  ```

- O(n):
  - Time complexity is O(n^2) because of the nested loops.
  - Space complexity is O(1) because no additional space is used.
- When to use:
- When not to use:

### Merge Sort
- It's a combination of two things - merging and sorting.
- Exploits the fact that arrays of 0 or 1 element are always sorted.
- Works by decomposing an array into smaller arrays of 0 or 1 elements, then building up a newly sorted array.

#### Merging Two Sorted Collections
- Given two collections which are sorted, this helper function should create a new array which is also sorted, and consists of all of the elements in the two input collections.
- The function responsible for merging two sorted arrays should run in O(n + m) time and O(n + m) space and should not modify the parameters passed to it.
- Steps:
  1. Create an empty collection, take a look at the smallest values in each input collection.
  2. While there are still values we haven't looked at
    - If the value in the first array is smaller than the value in the second array, push the value in the first array into our results and move in to the next value in the first array, or else push the value in the second array into our results and move in to the next value in the second array.
    - Once we exhaust one array, push in all remaining values from the other array.

    ```js
    function increaseIndex(arr, value, index) {
      arr.push(value);
      return index++;
    }

    // Solution 1: (mine)
    function merge(collection1, collection2) {
      const result = [];
      let i = 0;
      let j = 0;

      while(i < collection1.length || j < collection2.length) {
        if(i === collection1.length) {
          result.push(...collection2.slice(j));
          break;
        } else if(j === collection2.length) {
          result.push(...collection1.slice(i));
          break;
        }
      
        if(collection1[i] < collection2[j]) {
          i = increaseIndex(result, collection1[i], i);
        } else if(collection1[i] > collection2[j]) {
          j = increaseIndex(result, collection2[j], j);
        } else {
          i = increaseIndex(result, collection1[i], i);
          j = increaseIndex(result, collection2[j], j);
        }
      }

      return result;
    }

    // Solution 2:
    function merge(collection1, collection2) {
      const result = [];
      let i = 0;
      let j = 0;

      while(i < collection1.length && j < collection2.length) {
        if(collection1[i] < collection2[j]) {
          i = increaseIndex(result, collection1[i], i);
        } else if(collection1[i] > collection2[j]) {
          j = increaseIndex(result, collection2[j], j);
        } else {
          i = increaseIndex(result, collection1[i], i);
          j = increaseIndex(result, collection2[j], j);
        }
      }

      while(i < collection1.length) {
          i = increaseIndex(result, collection1[i], i);
      }

      while(j < collection2.length) {
          j = increaseIndex(result, collection2[j], j);
      }

      return result;
    }

    ```

- Steps:
  1. Break up the array into halves until you have arrays that are empty or have one element.
  2. Once you have smaller sorted arrays, merge those arrays with other sorted arrays until you are back at the full length of the array.
  3. Once the array has been merged back together, return the merged (and sorted! array)

```js
// Syntax
function mergeSort(collection) {
  if(collection.length === 1) {
    return collection;
  }
  
  const halfLength = Math.floor(collection.length);
  const left = mergeSort(collection.slice(0, halfLength));
  const right = mergeSort(collection.slice(halfLength));

  return merge(left, right);
}
```

- O(n):
  - Time complexity is O(nlogn).
  - Space complexity is O(n).

- When to use:
- When not to use:

### Quick Sort:
- Like merge sort, exploits the fact that arrays of 0 or 1 element are always sorted,
- Works by selecting one element (called the **pivot**) and finding the index where the pivot should end up in the sorted array;
- Once the pivot is positioned appropriately, quick sort can be applied on either side of the pivot.

#### Pivot
- Given an array, this helper function should designate an element as the pivot.
- It should then rearrange elements in the array so that all values less than the pivot are moved to the left of the pivot, and all values greater than the pivot are moved to the right of the pivot.
- The order of elements on either side of the pivot doesn't matter.
- The helper should do this in place, i.e. it should not create a new array.
- When complete, the helper should return the index of the pivot.
- Steps:
  1. It will help to accept three arguments: an array, a start index and an end index.
  2. Grab the pivot from the start of the array.
  3. Store the current pivot index in a variable for keeping track of where the pivot should end up
  4. Loop through the array from the start until the end.
    - If the pivot is greater than the current element, increment the pivot index variable and then swap the current element with the element at the pivot index.
  5. Swap the starting element (i.e. the pivot) with the pivot index
  6. Return the pivot index.

  ```js
  // Syntax
  function swap(arr, i, j) {
    const temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }

  function getPivotIndex(collection, startIndex = 0, endIndex = collection.length - 1) {
    const pivotIndex = startIndex;
    const pivot = collection[startIndex];
      
    for(let i = startIndex; i <= endIndex; i++) {
      if(pivot < collection[i + 1]) {
        pivotIndex++;
        swap(collection, pivotIndex, i + 1);
      }
    }
    swap(collection, startIndex, pivotIndex);

    return pivotIndex;
  }
  ```

  - Steps:
    1. Call the pivot with help of the pivot function that we have created.
    2. When the helper returns to you the updated pivot index, recursively call the pivot helper on the subarray to the left of that index, and the subarray to the right of that index.
    3. Your base case occurs when you consider a subarray with less than 2 elements.
  
  ```js
  // Syntax
  function quickSort(collection, startIndex = 0, endIndex = collection.length - 1) {
    if(startIndex < endIndex) {
      const pivotIndex = pivot(collection, startIndex, endIndex);

      // left
      quickSort(collection, startIndex, pivotIndex - 1);

      // right
      quickSort(collection, pivotIndex + 1, endIndex);
    }

    return collection;
  }
  ```
  
- O(n):
  - Time complexity is O(nlogn) or O(n^2) [worst].
  - Space complexity is O(n).

- When to use:
- When not to use:

### Radix Sort
- Radix sort is a special sorting algorithm that works on lists of numbers.
- It never makes comparisons between elements!
- It exploits the fact that information about the size of a number is encoded in the number of digits.
- More digits means a bigger number in radix sort.

  #### Get Digit Of A Number In Specific Place
  ```js
  // Syntax

  // Solution 1
  function getDigit(num, place) {
    const strNum = `${num}`;
    return +strNum[strNum.length - 1 - place];
  }

  // Solution 2
  function getDigit(num, place) {
    return Math.floor(Math.abs(num) / Math.pow(10, i)) % 10;
  }
  ```

  #### Get No Of Digits Of A Number
  ```js
  // Solution 1
  function digitCount(num) {
    let i = num;
    let count = 0;
    do {
        i = Math.floor(Math.abs(i) / 10);
        count++;
    } while(i > 0);
    
    return count;
  }

  // Solution 2
  function digitCount(num) {
    if(num === 0) return 1;

    return Math.floor(Math.log10(Math.abs(num))) + 1;
  }
  ```

  #### Get Most Digits In An Array
  ```js
  // Solution 1
  function mostDigits(arr) {
    let mostDigits = 0;
    for(let i = 0; i < arr.length; i++) {
      const count = digitCount(arr[i]);

      if(count > mostDigits) {
        mostDigits = count;
      }

      mostDigits = Math.max(mostDigits, digitCount(arr[i]));
    }

    return mostDigits;
  }

  // Solution 2
  function mostDigits(arr) {
    let mostDigits = 0;
    for(let i = 0; i < arr.length; i++) {
      mostDigits = Math.max(mostDigits, digitCount(arr[i]));
    }

    return mostDigits;
  }
  ```

- Steps:
  1. Define a function that accepts list of numbers.
  2. Figure out how many digits the largest number has.
  3. Loop from k = 0 up to this largest number of digits.
  4. For each iteration of the loop:
    - Create buckets for each digit (0 to 9)
    - place each number in the corresponding bucket based on its kth digit
  5. Replace out existing array with values in our buckets, starting with 0 and going up to 9
  6. Return list at the end.

```js
// Syntax
function radixSort(collection) {
  const maxNoOfDigits = mostDigits(collection);
  const result = collection;
  for(i = 0; i < maxNoOfDigits; i++) {
    const bucket = Array.from({length: 10}, () => []);

    for(j = 0; j < result.length; j++) {
      const nthPlacedDigits = getDigit(result[j], i);
      bucket[nthPlacedDigits].push(result[j]);
    }

    result = [].concat(...bucket);
  }

  return result;
}
```
  
- O(n):
  - Time complexity is O(nk).
  - Space complexity is O(n + k).

- When to use:
- When not to use: