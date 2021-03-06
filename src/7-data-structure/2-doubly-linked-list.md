# Doubly Linked List
- It consists of nodes where each node has a value and two pointers that points to previous or next node or null.
- It consists of **head**, **tail** and **length** property to keep track of lists.
- Like any array, there are no indexes in the list. So, it can't be accessed through index
- It is a bi-directional, that mean a node has knowledge of previous and next nodes

## Singly linked list vs Doubly linked list
| Single linked list | Doubly linked list |
| ------------------ | ----- |
| A node has one pointer which is connected to its next node | A node has two pointers which are connected to its previous and next nodes |

d828345
61b448a

## Operation
1. Push
- Adding a new node to the end of the Linked List!

```js
// Syntax
/*
  - Create a new node with the value passed to the function
  - If the head property is null set th head and tail to be the newly created node
  - If not, set the next property on the tail to be that node
  - Set the previous property on the newly created node to be the tail
  - Set the tail to be the newly created node
  - Increment the length by one
  - Return the linked list
*/
```

2. Pop
- Removing the node from the end of the linked list

```js
// Syntax
/*
  - If there is no head, return undefined
  - Store the current tail in a variable to return later
  - If the length is 1, set the head and tail to be null
  - Update the tail to be the previous node
  - Set the new tail's next to null
  - Decrement the length
  - Return the value removed
*/
```

3. Shift
- Add node to start of the linked list

```js
// Syntax
/*
  - If length is 0, return undefined
  - Store the current head property in a variable (we'll call it old head)
  - If the length is noe
    - set the head to be null
    - set the tail to be null
  - Update the head to be the next of the old head
  - Set the head's prev property to null
  - Set the old head's next to null
  - Decrement the length
  - Return old head
*/
```

4. Unshift
- Added new node to the beginning of the linked list.

```js
// Syntax
/*
  - Create a new node with the value passed to the function
  - If the length is 0
    - set the head to be the new node
    - set the tail to be the new node
  - Otherwise
    - set the prev property on the head of the list to be the new node
    - set the next property on the new node to be the head property
    - update the head to be the new node
  - Increment the length
  - Return the list
*/
```

5. Get
- Get the index value from the linked list

```js
// Syntax
/*
  - If the index is less than 0 or greater or equal to the length, return null
  - If the index is less than or equal to half the length of the list
    - loop through the list starting from the head and loop towards the middle
    - return the node once it is found
  - If the index is greater than half the length of the list
    - loop through the list starting from the tail and loop towards the middle
    - return the node once it is found
*/
```

6. Set
- Set the value of the node of the given index if exist

```js
// Syntax
/*
  - Create a variable which is the result of the get method at the index passed to the function
    - if the get method returns a valid node, set the value of the node to be the value passed to the function
    - return true
  - Otherwise, return false
*/
```

7. Insert
- Insert the node the the specific index

```js
// Syntax
/*
  - If the index is less than zero or greater than or equal to the length return false
  - If the index is 0, unshift
  - If the index is the same as the length, push
  - Use the get method to access the index - 1
  - Set the next and prev properties on the correct nodes to link everything together
  - Increment the length
  - Return true
*/
```

8. Remove
- Removed the node from the given index

```js
// Syntax
/*
  - If the index is less than zero or greater than or equal to the length return undefined
  - If the index is 0, shift
  - If the index is the same as the length - 1, pop
  - Use the get method to retrieve the item to be removed
  - Update the next and prev properties to remove the found node from the list
  - Set next next and prev to null on the found node
  - Decrement the length
  - Return the removed node
*/
```

## Big O
| Operation | Time Complexity | Space Complexity |
| --------- | --------------- | ---------------- |
| Insertion | O(1) | O(1) |
| Removal | O(1) | O(1) |
| Searching | O(N) | O(N) |
| Access | O(N) | O(N) |

```ts
/**
 * Class contains of leaf of node of singly linked list
 */
class ListNode<T> {
  public value: T;
  public next: ListNode<T>;
  public prev: ListNode<T>;

  constructor(value: T) {
    this.value = value;
    this.next = null;
    this.prev = null;
  }
}

/**
 * Class containing operation related to singly linked list
 */
class SinglyLinkedList<T> {
  private head: ListNode<T>;
  private tail: ListNode<T>;
  public length: number;

  constructor() {
    this.head = this.tail = null;
    this.length = 0;
  }

  /**
   * Checks if the list is empty or not
   */
  public get isEmpty() {
    return this.length === 0;
  }

  /**
   * Increase the length of list
   */
  private increaseLength = () => this.length++;

  /**
   * Sets the tracker of the list
   * @param {ListNode<T>} head - Head property of the list
   * @param {ListNode<T>} tail - Tail property of the list
   */
  private setListTracker = (tacker: {
    head?: ListNode<T>;
    tail?: ListNode<T>;
  }) => {
    const { head, tail } = tacker;

    if (head !== undefined) {
      this.head = head;
    }

    if (tail !== undefined) {
      this.tail = tail;
    }
  };

  private setNextNode = (nextNode: ListNode<T>) => {
    this.tail.next = nextNode;
    nextNode.prev = this.tail;
    this.setListTracker({
      tail: nextNode
    });
  }

  /**
   * Pushes the value at end of the list
   * @param {T} value - Value that needs to be pushed in the list
   * @returns {SinglyLinkedList<T>} - Instance of the SinglyLinkedList class
   */
  public push = (value: T) => {
    const newNode = new ListNode(value);

    if (this.isEmpty) {
      this.setListTracker({ head: newNode, tail: newNode });

      return this;
    }
    this.increaseLength();

    this.setNextNode(newNode);

    return this;
  };

  /**
   * Removes the last value from the list
   * @returns {ListNode<T>} - Removed value from the list if exists
   */
  public pop = () => {
    if (this.isEmpty) return null;

    this.decreaseLength();
    const temp = this.tail;

    if(this.tail.prev === null) {
      this.setListTracker({ head: null, tail: null });
      return temp;
    }

    this.tail = temp.prev;
    this.tail.next = null;
    temp.prev = null;

    return temp;
  };

  /**
   * Removes starting node of the list
   * @returns {ListNode<T>} - Removed value from the list if exists
   */
  public shift = () => {
    if (this.isEmpty) return undefined;

    const oldHead = this.head;
    
    if (this.length === 1) {
      this.setListTracker({ tail: null });
      return oldHead;
    }

    this.head = oldHead.next;
    this.head.prev = null;
    oldHead.next = null;
    this.decreaseLength();
    return oldHead;
  };

  /**
   * Inserts node in the start of the list
   * @param {T} value - Value that is to be inserted
   * @returns {SinglyLinkedList<T>} - Instance of the SinglyLinkedList class
   */
  public unshift = (value: T) => {
    const newNode = new ListNode(value);

    if (this.isEmpty) {
      this.setListTracker({ head: newNode, tail: newNode });
      return this;
    }
    this.increaseLength();
    this.head.prev = newNode;
    newNode.next = this.head;
    this.setListTracker({ head: newNode });

    return this;
  };

  /**
   * Gets the node from the list of particular index if exist
   * @param {number} index - Index from where the node is to be taken
   * @returns {ListNode<T>} - Node of the list if exist
   */
  public getValue = (index: number) => {
    if (this.isEmpty || index < 0 || index >= this.length) return null;

    let count, currentNode;

    if(index <= this.length / 2) {
      // Working from start
      counter = 0;
      currentNode = this.head;
      while (counter != index) {
        currentNode = currentNode.next;
        counter++;
      }
  
      return currentNode;
    }

    // Working from start
    count = this.length - 1;
    currentNode = this.tail;
    while(count !== index) {
      currentNode = currentNode.prev;
      count--;
    }

    return currentNode;
  };

  /**
   * Sets the value in specific index of the list
   * @param {T} value - Value which is to be set
   * @param {number} index - Index number where value of the node is to be set
   * @returns {boolean} - Boolean value the determines if the is set or not
   */
  public setValue = (value: T, index: number) => {
    const foundNode = this.getValue(index);

    if (foundNode) {
      foundNode.value = value;

      return true;
    }

    return false;
  };

  /**
   * Inserts the value in specific index of the list
   * @param {T} value - Value which is to be inserted
   * @param {number} index - Index number where value of the node is to be inserted
   * @returns {boolean} - Boolean value the determines if the is inserted or not
   */
  public insert = (value: T, index: number) => {
    if (this.isEmpty || index < 0 || index > this.length) return false;
    if (index === 0) return !!this.unshift(value);
    if ((index = this.length)) return !!this.push(value);

    const newNode = new ListNode(value);
    const beforeNode = this.getValue(index - 1);
    const afterNode = beforeNode.next;

    beforeNode.next = newNode;
    newNode.prev = beforeNode;
    newNode.next = afterNode;
    afterNode.prev = newNode;
    this.increaseLength();

    return true;
  };

  /**
   * Removes the node of the given index from the list
   * @param {number} index - Index value from where node is to be removed
   * @returns {ListNode<T>} - Node which is removed if exist
   */
  public remove = (index: number) => {
    if (index < 0 || index >= this.length) return undefined;
    if (index === 0) return this.shift();
    if (index === this.length - 1) return this.pop();

    const removedNode = this.getValue(index - 1);
    const beforeNode = removedNode.prev;
    const afterNode = removedNode.next;

    beforeNode.next = afterNode;
    afterNode.prev = beforeNode;

    removedNode.next = null;
    removedNode.prev = null;

    this.decreaseLength();

    return removedNode;
  };
}

```