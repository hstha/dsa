# Graphs
- A graph data structure consist of a finite (and possibly mutable) set of vertices or nodes or points, together with a set of unordered pairs of these vertices for an undirected graph or a set of ordered pairs for a directed graph.

## Usages of graph
- Social Networking
- Location / Mapping
- Routing Algorithms
- Visual Hierarchy
- File System Optimization
- and many more

## Terminology
1. `Vertex`: a node
2. `Edges`: connection between nodes
3. `Weighted` / `Unweighted`: values assigned to distances between vertices

> All though many DS can be used to create graph but `adjacency list` and `adjacency matrix` is widely used

## Adjacency List vs Adjacency Matrix
| Adjacency List | Adjacency Matrix |
| -------------- | ---------------- |
| Can take up less space (in sparse graphs) | Takes up more space (in sparse graphs) |
| Faster to iterate over all edges | Slower to iterate over all edges |
| Can be slower to lookup specific edge | Faster to lookup specific edge |

## Big 0
|V| - number of vertices
|E| - number of edges

| Operation | Adjacency List | Adjacency Matrix |
| --------- | -------------- | ---------------- |
| Add Vertex | O(1) | O(|V^2|) |
| Add Edge | O(1) | O(1) |
| Remove Vertex | O(|V| + |E|) | O(|V^2|) |
| Remove Edge | O(|E|) | O(1) |
| Query | O(|V| + |E|) | O(1) |
| Storage | O(|V| + |E|) | O(|V^2|) |

## Which is best Adjacency List or Matrix?
- If we have a sparse data than Adjacency list should be used or else use adjacency matrix
> In real world, most of the data are `sparse`

## Methods
1. Add Vertex
```js
// Syntax
/*
  - Write a method which accepts a name of a vertex
  - It should add a key to the list with the name of the vertex and set its value to be an empty array
*/
```

2. Add Edge
```js
// Syntax
/*
  - Create a function that accept two vertices, say v1 and v2
  - The function should find in the list the key of v1 and push v2 and vice-versa.
*/
```

3. Remove Edge
```js
// Syntax
/*
  - The function should accept two vertices, say v1 and v2
  - The function should reassign the key of vertex1 to be an array that does not contain vertex2 and vice-versa
*/
```

4. Remove Vertex
```js
// Syntax
/*
  - The function should accept a vertex to remove
  - The function should loop as long as there are any other vertices in the adjacency list for that vertex
  - Inside of the loop, call our removeEdge function with the vertex we are removing and any values in the adjacency list for that vertex
  - delete the key in the adjacency list for that vertex
*/
```

```ts
class Graph<T> {
  adjacencyList: any{};
  constructor() {
    // we can use heap too
    this.adjacencyList = {};
  }

  addVertex(vertexName: T) {
    if(!this.isVertexExist(vertexName)) {
      this.adjacencyList[vertexName] = [];
    }

    return this;
  }

  isVertexExist(vertexName: T) {
    return this.adjacencyList.hasOwnProperty(vertexName);
  }

  getVertexValue(vertexName: T) {
    return this.adjacencyList[vertexName];
  }

  setVertexValue(vertexName: T, values: T[]) {
    this.adjacencyList[vertexName] = values;
  }

  hasAnyVertexPresent(v1: T, v2: T) {
    return this.isVertexExist(v1) && this.isVertexExist(v2);
  }

  addEdge(v1: T, v2: T) {
    if(!this.hasAnyVertexPresent(v1, v2)) return false;

    const vertex1 = this.getVertexValue(v1);
    const vertex2 = this.getVertexValue(v2);

    if(!vertex1.includes(v2)) vertex1.push(v2);
    if(!vertex2.includes(v1)) vertex2.push(v1);
  }

  removeEdge(v1: T, v2: T) {
    if(!this.hasAnyVertexPresent(v1, v2)) return false;

    let vertex1 = this.getVertexValue(v1);
    let vertex2 = this.getVertexValue(v2);

    if(vertex1.includes(v2)) {
      vertex1 = vertex1.filter((vertex) => vertex !== v2);

      this.setVertexValue(v1, vertex1);
    }

    if(vertex2.includes(v1)) {
      vertex2 = vertex2.filter((vertex) => vertex !== v1);

      this.setVertexValue(v2, vertex2);
    }
  }

  removeVertex(vertex: T) {
    if(!this.isVertexExist(vertex)) return false;

    const vertexValue = this.getVertexValue(vertex);

    while(vertexValue.length) {
      const adjacentVertex = vertexValue.pop();
      this.removeEdge(vertex, adjacentVertex);
    }
    delete this.adjacency[vertex];

    return this;
  }
}
```

## Graph Traversal
- Traversal meaning visiting. updating, checking vertexes

### Graph Traversal uses
- Peer to peer networking
- Web crawlers
- Finding "closest" matches/recommendations
- Shortest path problems
  - GPS Navigation
  - Solving mazes
  - AI (shortest path to win the game)

### Depth First Traversal
```js
// Syntax (Recursive)
/*
  - Create a function that accepts starting vertex
  - If vertex is empty than return "this is base case"
  - Add vertex to results list
  - Mark vertex as visited
  - For each neighbor in vertex's neighbors:
    - If neighbor is not visited:
      - recursively call DFS on neighbor
*/
```

```ts
function dfs_traverse<T>(starting_vertex: T) {
  const results: T[] = [];
  const visited: T[] = [];

  const dfs = (vertex) => {
    if(!vertex) return;

    results.push(vertex);
    visited.push(vertex);

    for(let i = 0; i <= this.adjacencyList; i++) {
      if(!visited.includes(this.adjacencyList[i])) {
        dfs(vertex);
      }
    }
  }

   dfs(starting_vertex) 

  return results;
}
```

```js
// Syntax (Iterative)
/*
  - Create a function that accepts starting vertex
  - Create a stack
  - Push the given vertex into stack
  - while stack is not empty
    - Pop the stack
    - mark that vertex as visited
    - if the popped vertex is not labeled as discovered,
      - add that vertex in result list
      - for each of vertex's neighbors, push those vertex into stack
*/
```

```ts
function dfs_traverse<T>(starting_vertex: T) {
  const results: T[] = [];
  const visited: T[] = [];
  const stack = new Stack<T>();

  stack.push(starting_vertex);
  while(stack.length) {
    const vertex = stack.pop();
    results.push(vertex);

    if(!visited.incudes(vertex)) {
      visited.push(vertex);

      this.adjacencyList[vertex].forEach(node => {
        stack.push(node);
      });
    }
  }

  return results;
}
```

### Breath First Traversal
```js
// Syntax
/*
- Function that accepts a starting vertex
- Create a queue (you can use an array) and place the starting vertex in it
- Create an array to store the nodes result
- Create an array to store the visited nodes
- Mark the starting vertex as visited

- Loop as long as there is anything in the queue
  - Remove the first vertex from the queue and push it into the array that stores nodes result
  - Loop over each vertex in the adjacency list for the vertex you are visiting.
    - If it is not inside the object that stores nodes visited, mark it as visited and enqueue that vertex
- Once you have finished looping, return the array of visited nodes.
*/
```

```ts
function breadthFirst<T>(start_vertex: T) {
  const queue = new Queue<T>();
  queue.enqueue(start_vertex);

  const result: T[] = [];
  const visited: T[] = [];
  let currentVertex: T;

  while(queue.length) {
    currentVertex = queue.dequeue();
    result.push(currentVertex);

    this.adjacencyList[currentVertex].forEach(neighbor => {
      if(!visited.includes(neighbor)) {
        visited.push(neighbor);
        queue.enqueue(neighbor);
      }
    });
  }

  return result; 
}
```

## Dijkstra's Algorithm
- Finds the shortest path between two vertices on a graph.

### Why it is important?
- It is used in various application like
  - GPS - `finding fastest route`
  - Network Routing - `finds open shortest path for data`
  - Biology - `used to model the spread of viruses among humans`
  - Airline tickets - `finding cheapest route to your destination`
  - Many other uses!

### Approach
- Every time we look to visit a new node, we pick the node with the smallest known distance to visit first.
- Once we've moved to the node we're going to visit, we look at each of its neighbors
- For each neighboring node, we calculate the distance by summing the total edges that lead to the node we're checking from the starting node.
- If the new total distance to a node is less than the previous total, we store the new shorter distance for that node.

```js
// Syntax
/*
  - Create a function should accept a starting and ending vertex
  - Create an object (we'll call it distances) and set each key to be every vertex in the adjacency list with a value of infinity, except for the starting vertex which should have a value of 0
  - After setting a value in the distances object, add ech vertex with a priority of infinity to the priority queue, except the starting vertex, which should have a priority of 0 because that's where we begin
  - Create another object called previous and set each key to be every vertex in the adjacency list with a value of null
  - Start looping as long as there is anything in the priority queue
    - dequeue a vertex from the priority queue
    - If that vertex is the same as the ending vertex, we are done
    - Otherwise loop through each value in the adjacency list at that vertex
      - Calculate the distance to that vertex from the starting vertex
      - If the distance is less than what is currently stored in our distances object
        - update the distances object with new lower distance
        - update the previous object to contain that vertex
        - enqueue the vertex with the total distance from the start node
*/
```

```ts
class WeightedGraph<T> {
  adjacencyList: any{};

  constructor() {
    this.adjacencyList = {};
  }

  getVertexEdges(vertex: T) {
    return this.adjacencyList[vertex];
  }

  addVertex(vertex: T) {
    if(!this.getVertexEdge(vertex)) this.adjacencyList[vertex] = [];
  }

  addEdge(vertex1: T, vertex2: T, weight: number) {
    this.adjacencyList[vertex1].push({node: vertex2, weight});
    this.adjacencyList[vertex2].push({node: vertex1, weight});
  }
}

function dijkstra<T>(start: T, finish: T, graph: WeightedGraph<T>) {
  const nodes = new PriorityQueue<T>();
  const distances = {};
  const previous = {};
  let path: T[] = [];
  let smallest: T; 

  // build up initial state 
  for(let vertex in this.adjacencyList) {
    if(vertex === start) {
      distance[vertex] = 0;
      nodes.enqueue(vertex, 0);
    } else {
      distances[vertex] = Infinity;
      nodes.enqueue(vertex, Infinity);
    }

    previous[vertex] = null;
  }

  // as long as there is something to visit
  while(nodes.heap.length) {
    smallest = nodes.dequeue();

    if(smallest === finish) {
      // we ar done
      // build up path to return at end
      while(previous[smallest]) {
         .push(smallest);
        smallest = previous[smallest];
      }
      break;
    } else if(smallest || distances[smallest] !== Infinity) {
      for(let neighbor in graph.adjacencyList[smallest]) {
        // find neighboring node
        let nextNode = graph.adjacencyList[smallest][neighbor];

        // calculate new distance to neighboring node
        let candidate = distance[smallest] + nextNode.weight;
        let nextNeighbor = nextNode.node;
        if(candidate < distance[nextNeighbor]) {
          // updating new smallest distance to neighbor
          distance[nextNeighbor] = candidate;
          // updating previous - How we got to neighbor
          previous[nextNeighbor] = smallest;
          // enqueue in priority queue with new priority
          nodes.enqueue(nextNeighbor, candidate);
        }
      }
    }
  }

  return path.concat(smallest).reverse();
}
```