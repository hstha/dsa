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
- Bubble Sort
- Selection Sort
- Insertion Sort
- Merge Sort
- Quick Sort
- Heap Sort
- Radix Sort

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
