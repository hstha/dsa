# Tree
- A data structure that consists of nodes in a parent/child relationship
- In a tree each node is moving away from the root node i.e each node has distinct children.
- Tree has only one entry point i.e a root node

## Terminologies
1. `Root`: The top node in a tree. Each tree has only one node
2. `Child`: A node directly connected to another node when moving away from the root.
3. `Parent`: THe converse notion of a child
4. `Siblings`: A group of nodes with the same parent
5. `Leaf`: A node with no children
6. `Edge`: THe connection between one node and another

## Tree Vs List
- List is a linear in structure whereas tree is a non-linear in structure

## Where Stacks are used?
- HTML DOM
- Network Routing
- Abstract Syntax Tree
- Artificial Intelligence
- Folders in OS
- Computer in File Systems

## Types of tree:
1. Binary Tree

### Binary Tree
- It is tree where each node has at most two children

#### Binary Search Tree (BST)
- It is a type of binary tree which are sorted in a particular order
- BST are generally used for comparing purpose
- In BST, 
  - Every node to the left of a parent is **always less** than the parent
  - Every node to the right of a parent node is **always greater** than the parent

##### Where BST is used
- Like the name, it is used for searching purpose

##### Methods
1. `Insert`:
```js
  // Syntax
  /*
    - Create a new node
    - Starting at the root
      - Check if there is a root, if not - the root now becomes that new node
      - If there is a root, check if the value of the new node is greater than or less than the value of the root
        - If it is greater,
          - Check to see if there is a node to the right
            - If there is, move to that node and repeat these steps
            - If there is not, add that node as the right property
        - If it is less
          - Check to if there is a node to the left
            - If there is, move to that node and repeat these steps
            - If there is not, add that node as the left property
  */
```

2. Find
```js
  // Syntax
  /*
    - Starting at the root
    - check if there is root, if not - we're done searching!
      - If there is a root, check if the value of the new node is the value we are looking for. If we found it, we're done
      - If not, check to see if the value is greater than or less than the value of the root
      - If it is greater
        - Check to see if there is a node to the right
          - If there is, move to that node and repeat these steps
          - If there is not we're done searching
      - If it is less
        - Check to see if there is node to the left
          - If there is, move to that node and repeat these steps
          - If there is not, we're done searching
  */
```

##### Big O
| Method | Time | Space |
| ------ | ---- | ----- |
| Insertion | O(log(N)) / O(n) `[worst]` | O(log(N)) / O(n) `[worst]` |
| Searching | O(log(N)) / O(n) `[worst]` | O(log(N)) / O(n) `[worst]` |

```ts
class Node<T> {
  value: T;
  left: Node<T> | null;
  right: Node<T> | null;

  constructor(value: T) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

class BTS<T> {
  root: Node<T> | null;

  constructor() {
    this.root = null;
  }

  find(value: T) {
    let currentNode = this.root;
    while(true) {
      if(!currentNode) {
        break;
      } else if(currentNode.value === value) {
        break;
      } else if(value > currentNode.value) {
        currentNode = currentNode.right;
      } else if(value < currentNode.value) {
        currentNode = currentNode.left;
      }
    }

    return currentNode ? currentNode : undefined;
  }

  insert(value: T) {
    const newNode = new Node(value);

    if(this.root === null) {
      this.root = newNode;
      return this;
    }

    let currentNode = this.root;
    while(true) {
      if(value < currentNode.value) {
        if(currentNode.left === null) {
          currentNode.left = newNode;
          break;
        }

        currentNode = currentNode.left;
      } else {
        if(currentNode.right === null) {
          currentNode.right = newNode;
          break;
        }

        currentNode = currentNode.right;
      }
    }

    return this;
  }
}
```