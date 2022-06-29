# Singly Linked Lists
- It consists of nodes where each node has a value and a pointer that points to another node or null.
- It consists of **head**, **tail** and **length** property to keep track of lists.
- Like any array, there are no indexes in the list. So, it can't be accessed through index
- It is a uni-directional, that mean a node has knowledge of another node that is a head of it not vice-versa.

## Singly linked list vs Array
| Single linked list | Array |
| ------------------ | ----- |
| Don't have indexes | Indexed in order |
| Connected via nodes with a next pointer | No nodes |
| Random access is not allowed | Can quickly be accessed at a specific index |
| Insertion and deletion is not expensive | Insertion and deletion can be expensive |

## Operation
1. Push
- Adding a new node to the end of the Linked List!

```js
// Syntax
/*
  - This function should accept a value
  - Create a new node using the value passed to the function
  - If there is no head property on the list, set the head and tail to be the newly created node
  - Otherwise set the next property on the tail to be the new node and set the tail property on the list to be the newly created node
  - Increment the length by one
  - Return the linked list
*/
```

2. Pop
- Removing a node from the end of the Linked List!

```js
// Syntax
/*
  - If there are no nodes in the list, return undefined
  - Loop through the list until you reach the tail
  - Set the next property of the 2nd to last node to be null
  - Set the tail to be the 2nd to last node
  - Decrement the length of the list by 1
  - Return the value of the node removed
*/
```

3. Shift
- Removing a new node from the beginning of the Linked List!

```js
// Syntax
/*
  - If there are no nodes, return undefined
  - Store the current head property in a variable
  - Set the head property to be the current head's next property
  - Decrement the length by 1
  - Return the value of the node removed
*/
```

4. Unshift
- Adding a new node to the beginning of the Linked List!

```js
// Syntax
/*
  - This function should accept a value
  - Create a new node using the value passed to the function
  - If there is no head property on the list, set the head and tail to be the newly created node
  - Otherwise set the newly created node's next property to be the current head property on the list
  - Set the head property on the list to be that newly created node
  - Increment the length of the list by 1
  - Return the linked list
*/
```

5. Get value
- Retrieving a node by it's position in the Linked List!

```js
// Syntax
/*
  - This function should accept an index
  - If the index is less than zero or greater than or equal to the length of the list, return null
  - Loop through the list until you reach the index and return the node at that specific index
*/
```

6. Set value
- Changing the value of a node based on it's position in the Linked List

```js
// Syntax
/*
  - This function should accept a value and an index
  - Use your get function to find the specific node.
  - If the node is not found, return false
  - If the node is found, set the value of that node to be the value passed to the function and return true
*/
```

7. Insert
- Adding a node to the Linked List at a specific position

```js
// Syntax
/*
  - If the index is less than zero or greater than the length, return false
  - If the index is the same as the length, push a new node to the end of the list
  - If the index is 0, unshift a new node to the start of the list
  - Otherwise, using the get method, access the node at the index - 1
  - Set the next property on that node to be the new node
  - Set the next property on the new node to be the previous next
  - Increment the length
  - Return true
*/
```

8. Remove
- Removing a node from the Linked List at a specific position

```js
// Syntax
/*
  - If the index is less than zero or greater than the length, return undefined
  - If the index is the same as the length-1, pop
  - If the index is 0, shift
  - Otherwise, using the get method, access the node at the index - 1
  - Set the next property on that node to be the next of the next node
  - Decrement the length
  - Return the value of the node removed
*/
```

9. Reverse
- Reversing the Linked List in place!

```js
// Syntax
/*
  - Swap the head and tail
  - Create a variable called next
  - Create a variable called prev
  - Create a variable called node and initialize it to the head property
  - Loop through the list
  - Set next to be the next property on whatever node is
  - Set the next property on the node to be whatever prev is
  - Set prev to be the value of the node variable
  - Set the node variable to be the value of the next variable
  - Once you have finished looping, return the list
*/
```

## Big O
| Operation | Time Complexity | Space Complexity |
| --------- | --------------- | ---------------- |
| Insertion | O(1) | O(1) |
| Removal | O(1) or O(N) | O(1) |
| Searching | O(N) | O(N) |
| Access | O(N) | O(N) |

```ts
/**
 * Class contains of leaf of node of singly linked list
 */
class ListNode<T> {
  public value: T;
  public next: ListNode<T>;

  constructor(value: T) {
    this.value = value;
    this.next = null;
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
   * Decrease the length of list
   */
  private decreaseLength = () => this.length--;

  /**
   * Checks if the node contains next node or not
   */
  private hasNext = (node: ListNode<T>) => !!node.next;

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

  /**
   * Pushes the value at end of the list
   * @param {T} value - Value that needs to be pushed in the list
   * @returns {SinglyLinkedList<T>} - Instance of the SinglyLinkedList class
   */
  public push = (value: T) => {
    const newNode = new ListNode(value);
    this.increaseLength();

    if (this.isEmpty) {
      this.setListTracker({ head: newNode, tail: newNode });

      return this;
    }

    this.tail.next = newNode;
    this.setListTracker({ tail: newNode });

    return this;
  };

  /**
   * Loops through elements of the list
   * @param {ListNode<T>} head - Node of the list
   * @param {Function} cb - A callback function that runs with list node as parameter and returns boolean value to check if it can break out of loop or not
   */
  private loop = (head: ListNode<T>, cb: (node: ListNode<T>) => boolean) => {
    let currentNode = head;

    do {
      if (cb(currentNode)) {
        break;
      }
    } while (this.hasNext(currentNode));
  };

  /**
   * Removes the last value from the list
   * @returns {ListNode<T>} - Removed value from the list if exists
   */
  public pop = () => {
    if (this.isEmpty) return null;

    let newTail = this.head;
    let currentNode = this.head;

    this.loop(this.head, (node) => {
      newTail = node;
      currentNode = node.next;

      return false;
    });

    // do {
    //   newTail = currentNode;
    //   currentNode = currentNode.next;
    // } while (this.hasNext(currentNode));

    this.decreaseLength();

    if (this.isEmpty) {
      this.setListTracker({ tail: null, head: null });

      return currentNode;
    }

    this.setListTracker({ tail: newTail });
    this.tail.next = null;

    return currentNode;
  };

  /**
   * Removes starting node of the list
   * @returns {ListNode<T>} - Removed value from the list if exists
   */
  public shift = () => {
    if (this.isEmpty) return null;

    const currentHead = this.head;
    this.head = currentHead.next;
    this.decreaseLength();

    if (this.length === 0) {
      this.setListTracker({ tail: null });
    }

    return currentHead;
  };

  /**
   * Inserts node in the start of the list
   * @param {T} value - Value that is to be inserted
   * @returns {SinglyLinkedList<T>} - Instance of the SinglyLinkedList class
   */
  public unshift = (value: T) => {
    const newNode = new ListNode(value);
    this.increaseLength();

    if (this.isEmpty) {
      this.setListTracker({ head: newNode, tail: newNode });
      return this;
    }

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

    let counter = 0;
    let currentNode = this.head;

    while (counter != index) {
      currentNode = currentNode.next;
      counter++;
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
    const prevNode = this.getValue(index - 1);
    const temp = prevNode.next;
    prevNode.next = newNode;
    newNode.next = temp;
    this.increaseLength();

    return true;
  };

  /**
   * Removes the node of the given index from the list
   * @param {number} index - Index value from where node is to be removed
   * @returns {ListNode<T>} - Node which is removed if exist
   */
  public remove = (index: number) => {
    if (index < 0 || index >= this.length) return null;
    if (index === 0) return this.shift();
    if (index === this.length - 1) return this.pop();

    const previousNode = this.getValue(index - 1);
    const removed = previousNode.next;
    previousNode.next = removed.next;
    this.decreaseLength();

    return removed;
  };

  /**
   * Reverses the given list
   * @returns {SinglyLinkedList} - Instance of SinglyLinkedList
   */
  public reverse = () => {
    let node = this.head;
    this.head = this.tail;
    this.tail = node;
    let next: ListNode<T>;
    let prev: ListNode<T> = null;

    for (let i = 0; i < this.length; i++) {
      next = node.next;
      node.next = prev;
      prev = node;
      node = next;
    }

    return this;
  };

  /**
   * Checks if the value is exist or not in the list
   * @param {Function} cb - Callback function to check if it exist in the list or not
   * @returns {boolean} - Boolean value that determines if the value is included in the list or not
   */
  public includes = (cb: (value: T) => boolean) => {
    let isIncluded = false;

    if (this.isEmpty) return isIncluded;

    this.loop(this.head, (node) => {
      if (cb(node.value)) {
        isIncluded = true;
        return true;
      }

      node = node.next;

      return false;
    });

    // let currentNode = this.head;

    // do {
    //   if (cb(currentNode.value)) {
    //     isIncluded = true;
    //     break;
    //   }

    //   currentNode = currentNode.next;
    // } while (this.hasNext(currentNode));

    return isIncluded;
  };

  /**
   * Converts list to collection
   * @returns {Array} - Collection of the values from the list
   */
  public get toArr() {
    let arr: T[] = [];

    if (this.isEmpty) return arr;

    this.loop(this.head, (node) => {
      arr.push(node.value);
      node = node.next;

      return false;
    });

    // let currentNode = this.head;

    // do {
    //   arr.push(currentNode.value);
    //   currentNode = currentNode.next;
    // } while (this.hasNext(currentNode));

    return arr;
  }

  /**
   * Creates Singly Linked List from the collection
   * @param {T[]} arr - Collection of T type
   * @returns {SinglyLinkedList} - Instance of SinglyLinkedList
   */
  public static fromArr = <T>(arr: T[]) => {
    const list = new SinglyLinkedList<T>();

    for (const element of arr) {
      list.push(element);
    }

    return list;
  };
}

```