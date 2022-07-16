# Binary Heaps
- Binary heaps is similar to a binary search tree, but with some different rules i.e parent node can be greater or smaller than its children.
- There is no guarantees between sibling nodes.
- A binary heap is as compact as possible. All the children of each node are as full as they can be and left children are filled out first

## Why do we need to know binary heaps?
- Binary Heaps are used to implement `Priority Queues`
- They are also used quite a bit, with `graph traversal` algorithms

> For given data in a collection for binary heaps, if `n` be any index of a parent in the collection, than its `left` and `right` children are stored at `2n + 1` and `2n + 2` index respectively.

> For given data in a collection for binary heaps, if `n` be any index of a child in the collection, than its parent is at `Math.floor((n - 1) / 2)` index.

## Binary Heap vs BTS


## Type of binary heaps
1. `MaxBinaryHeap`:
2. `MinBinaryHeap`: 

### MaxBinaryHeap:
- In a **MaxBinaryHeap**, parent nodes are always larger than child nodes.

- Methods:
  1. Insert:
  - When we add the value to the end of the collection and bubble it up until it reaches it's respective place

  ```js
    // Syntax
    /*
      - Push the value into the collection property on the heap
      - Bubble up:
        - Create a variable called index which is the length of the values property - 1.
        - Create a variable called parentIndex which is the floor of (index - 1) / 2.
        - Keep looping as long as the values element at the parentIndex is less than the values element at the child index
          - Swap the value of the values element at the parentIndex with the value of the element property at the child index
          - Set the index to be the parentIndex and start over
    */
  ```

  2. Remove:
    - Remove the maximum value from the heap i.e root and replace it with most recently added node and adjust i.e sink down
    
    ```js
      // Syntax
      /*
        - Swap the first value in heap with the last one
        - Pop from the heap, so you can return the value at the end
        - Have the new root "sink down" to the correct spot
          - Your parent index starts at 0 (the root)
          - Find the index of the left child and make sure it is not out of bounds
          - Find the index of the right child and make sure it is not out of bounds
          - If the left or right child is greater than the element, swap. If both children are larger, swap with the largest child
          - The child index you swapped to now becomes the new parent index.
          - Keep looping and swapping until neither child is larger than the element.
          - Return the old root!
      */
    ```

- Big O
  - Heap excel on insertion and removal but not used for searching purpose
| Method | Time | Space |
| ------ | ---- | ----- |
| Insertion | O(log(N)) | O(log(N)) |
| Removal | O(log(N)) | O(log(N)) |
| Searching | O(N) | O(N) |

```ts
class MaxBinaryHeap<T> {
  heap: T[];

  constructor() {
    this.heap = [];
  }

  enque(value: T) {
    this.heap.push(value);
    this.bubbleUp();

    return this;
  }

  bubbleUp() {
    let index = this.heap.length - 1;
    const element = this.heap[index];

    while(index > 0) {
      let parentIndex = Math.floor((index - 1) / 2);
      let parent = this.heap[parentIndex];
      if(element <= parent) break;
      this.heap[parentIndex] = element;
      this.heap[index] = parent;
      index = parentIndex;
    }
  }

  remove() {
    const max = this.heap[0];
    const end = this.heap.pop();

    if(this.heap.length === 0) return max;

    this.heap[0] = end;
    this.sinkDown();

    return max;
  }

  sinkDown() {
    let index = 0;
    const length = this.heap.length;
    const element = this.heap[0];
    while(true) {
      let leftChildIndex = 2 * index + 1;
      let rightChildIndex = 2 * index + 2;
      let leftChild, rightChild;
      let swap = null;

      if(leftChildIndex < length) {
        leftChild = this.heap[leftChildIndex];
        if(leftChild > element) {
          swap = leftChildIndex;
        }
      }

      if(rightChildIndex < length) {
        rightChild = this.heap[rightChildIndex];
        if(
          (swap === null && rightChild > element) || (swap !== null && rightChild > leftChild)
        ) {
          swap = rightChildIndex;
        }
      }

      if(swap === null) break;
      this.heap[index] = this.heap[swap];
      this.heap[swap] = element;

      index = swap;
    }
  }
}
```

### MinBinaryHeap:
- In a **MinBinaryHeap**, parent nodes are always smaller than child nodes.

## Priority Queue
- A data structure where each element has a priority associated with it. 
- Elements with higher priorities are served before elements with lower priorities.
- It is just a concept, not necessarily implement with heap. But using heap is more efficient than other

```ts
class Node<T> {
  value: T;
  priority: number;

  constructor(value: T, priority: number = 5) {
    this.value = value;
    this.priority = priority;
  }
}

/*Implemented using minimum binary heap*/
class PriorityQueue<T> {
  heap: T[];
  
  constructor() {
    this.heap = [];
  }

  enqueue(value: T, priority: number) {
    const newNode = new Node(value, priority);
    this.heap.push(newNode);
    this.bubbleUp();

    return this;
  }

  bubbleUp() {
    let index = this.heap.length - 1;
    const element = this.heap[index];

    while(index > 0) {
      let parentIndex = Math.floor((index - 1) / 2);
      let parent = this.heap[parentIndex];
      if(element.priority >= parent.priority) break;
      this.heap[parentIndex] = element;
      this.heap[index] = parent;
      index = parentIndex;
    }
  }

  dequeue() {
    const min = this.heap[0];
    const end = this.heap.pop();

    if(this.heap.length === 0) return min;

    this.heap[0] = end;
    this.sinkDown();

    return min;
  }

  sinkDown() {
    let index = 0;
    const length = this.heap.length;
    const element = this.heap[0];
    while(true) {
      let leftChildIndex = 2 * index + 1;
      let rightChildIndex = 2 * index + 2;
      let leftChild, rightChild;
      let swap = null;

      if(leftChildIndex < length) {
        leftChild = this.heap[leftChildIndex];
        if(leftChild.priority > element.priority) {
          swap = leftChildIndex;
        }
      }

      if(rightChildIndex < length) {
        rightChild = this.heap[rightChildIndex];
        if(
          (swap === null && rightChild.priority < element.priority) || 
          (swap !== null && rightChild.priority < leftChild.priority)
        ) {
          swap = rightChildIndex;
        }
      }

      if(swap === null) break;
      this.heap[index] = this.heap[swap];
      this.heap[swap] = element;

      index = swap;
    }
  }
}
```