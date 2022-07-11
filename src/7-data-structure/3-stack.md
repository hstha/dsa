# Stack
- Stack is an abstract data collection that follows LIFO data structure.

## Where Stacks are used?
- Managing function invocations
- Undo / Redo
- Routing (the history object) is treated like a stack

## Methods:
- `Push`:
  - Have constant runtime.
  - Similar to unshift method of `singly linked list`.

  ```js
    // Syntax
    /*
      - The function should accept a value
      - Create a new node with the value
      - If there are no nodes in the stack, set the first and last property to be the newly created node.
      - If there is at least one node, create a variable that stores the current first property on the stack
      - Reset the first property to be the newly created node
      - Set the next property on the node to be the previously created variable
      - Increment the size of the stack by 1 and return it.
    */
  ```

- `Pop`:
  - Have constant runtime.
  - Similar to shift method of `singly linked list`.

  ```js
    // Syntax
    /*
      - If there are nodes in the stack, return null.
      - Create a temporary variable to store the first property on the stack
      - If there is only 1 node, set the first and last property to be null
      - If there is more than one node, set the first property to be the next property on the current first
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

  push(value: T) {
    this.stack.unshift(value);
    return this.stack.length;
  }

  pop() {
    const removedNode = this.stack.shift();

    return removedNode ? removedNode.value : null;
  }
}
```