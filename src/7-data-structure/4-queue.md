# Stack
- Stack is an abstract data collection that follows FIFO data structure.

## Where Stacks are used?
- Background tasks
- Uploading resources in general
- Printing / Task processing
- Processing the request

## Methods:
- `Enqueue`:
  - Have constant runtime.
  - Similar to `push` method of `singly linked list`.

  ```js
    // Syntax
    /*
      - The function should accept a value
      - Create a new node with the value
      - If there are no nodes in the queue, set the first and last property to be the newly created node.
      - Otherwise, set the next property on the current last to be that node, and then set the last property of the queue to be that node
      - Increment the size of the stack by 1 and return it.
    */
  ```

- `Dequeue`:
  - Have constant runtime.
  - Similar to `shift` method of `singly linked list`.

  ```js
    // Syntax
    /*
      - If there are nodes in the queue, return null.
      - Store the first property in a variable
      - See if the first is the same as the last (check if there is only 1 node). If so, set the first and last to be null
      - If there is more than 1 node, set the first property to be the next property of first
      - Decrement the size by 1
      - Return the value of the node removed
    */
  ```

`Note`: Searching and Access is not so important methods of stack, it generation focus on Insertion and Removal

## Big O
| Method | Space | Time |
| ------ | ----- | ---- |
| Insertion | O(1) | O(1) |
| Removal | O(1) | O(1) |
| Searching | O(N) | O(N ) |
| Access | O(N) | O(N ) |

```ts
class Stack<T> {
  private stack: SinglyLinkedList<T>;

  constructor() {
    this.stack = new SinglyLinkedList<T>();
  }

  enqueue(value: T) {
    this.stack.unshift(value);
    return this.stack.length;
  }

  dequeue() {
    const removedNode = this.stack.shift();

    return removedNode ? removedNode.value : null;
  }
}
```