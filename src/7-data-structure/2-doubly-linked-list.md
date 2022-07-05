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
}

```