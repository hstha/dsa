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
```

```ts
class Tree<T> {
  root: Node<T> | null;

  constructor() {
    this.root = null;
  }

  setRoot(node: Node<T>) {
    this.root = node;
    return this;
  }

  get hasRoot() {
    return this.root !== null;
  }

  insert(value: T) {
    const newNode = new Node(value);

    if(!this.hasRoot) {
      return this.setRoot(newNode);
    }

    // TODO: logic to insert the node to related parent
  }
}
```

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
class BTS<T> extends Tree<T> {
  constructor() {
    super();
  }

  find(value: T) {
    let currentNode = super.root;
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

    if(!super.hasRoot) {
      super.root = newNode;
      return this;
    }

    let currentNode = super.root;
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

## Tree Traversal
- Tree traversal means visiting the node only once until the given data is found
- Generally tree can be traversed in depth and breath first search

### Breath First Search (BFS)
- In this type of search, we visit every sibling nodes first before visiting at a child node.

```js
  // Syntax
  /*
    - Create a queue (this can be an array) and variable to store the values of nodes visited
    - Place the root node in the queue
    - Loop as long as there is anything in the queue
      - Dequeue a node from the queue and push the value of the node into the variable that stores the nodes
      - If there is a left property on the node dequeued - add it to the queue
      - If there is a right property on the node dequeued - add it to the queue
    - Return the variable that stores the values
  */
```

```ts
function bts<T>(tree: Tree<T>) {
  const data: T[] = [];
  const queue: T[] = new Queue<Node<T>>();
  let node = tree;
  queue.enqueue(node);

  while(queue.length) {
    node = queue.dequeue();
    data.push(node.value);

    // Enqueuing children of node from left to right fashion
    // Here assuming the tree is binary tree
    if(node.left) queue.enqueue(node.left);
    if(node.right) queue.enqueue(node.right);
  }

  return data;
}
```

### Depth First Search (DFS)
- In this type of search, we visit all the nodes vertically down to the end of the tree of the given node before moving to other sibling nodes
- DFS can be performed in three ways `pre-order`, `post-order`, `in-order`

#### PreOrder
- Here we first visit the parent node and start moving to one of its children vertically down until we reach leaf node before moving to the sibling nodes

```js
  // Syntax
  /*
    - Create a variable to store the values of nodes visited
    - Write a helper function which accepts a node
      - Push the value of the node to the variable that stores the values
      - call the helper function for all the direct children of that node
      [In case of binary tree]
        - If the node has a left property, call the helper function with the left property on the node
        - If the node has a right property, call the helper function with the right property on the node
    - Invoke the helper function with tree you want to traverse
    - Return the array of values
  */
```

```ts
function dfsPreOrder<T>(tree: Tree<T>) {
  const visitedNodes = [];
  function traverse(node: Tree<T>) {
    visitedNodes.push(node.value);

    // Assuming the node is binary tree
    if(node.left) traverse(node.left);
    if(node.right) traverse(node.right);
  }

  traverse(this.root);

  return visitedNodes;
}
```

#### PostOrder
- In post order, we visit the all the children nodes first before visiting their parent node

```js
  // Syntax
  /*
    - Create a variable to store the values of nodes visited
    - Write a helper function which accepts a node
      - call the helper function for all the direct children of that node
      [In case of binary tree]
        - If the node has a left property, call the helper function with the left property on the node
        - If the node has a right property, call the helper function with the right property on the node
      - Push the value of the node to the variable that stores the values
    - Invoke the helper function with tree you want to traverse
    - Return the array of values
  */
```

```ts
function dfsPostOrder<T>(tree: Tree<T>) {
  const visitedNodes = [];
  function traverse(node: Tree<T>) {
    // Assuming the node is binary tree
    if(node.left) traverse(node.left);
    if(node.right) traverse(node.right);
    visitedNodes.push(node.value);
  }

  traverse(this.root);

  return visitedNodes;
}
```

#### InOrder

```js
  // Syntax
  /*
    - Create a variable to store the values of nodes visited
    - Write a helper function which accepts a node
      - call the helper function for all the direct children of that node
      [In case of binary tree]
        - If the node has a left property, call the helper function with the left property on the node
        - Push the value of the node to the variable that stores the values
        - If the node has a right property, call the helper function with the right property on the node
    - Invoke the helper function with tree you want to traverse
    - Return the array of values
  */
```

```ts
function dfsInOrder<T>(tree: Tree<T>) {
  const visitedNodes = [];
  function traverse(node: Tree<T>) {
    // Assuming the node is binary tree
    if(node.left) traverse(node.left);
    visitedNodes.push(node.value);
    if(node.right) traverse(node.right);
  }

  traverse(this.root);

  return visitedNodes;
}
```

### BFS vs DFS. When to use?
- Since the time complexity of both BFS and DFS is similar. But the space complexity changes depending upon the situation

| BFS | DFS |
| --- | --- |
| when the given tree is very deep than that of its width | when the given tree is widely fleshed out than its depth |