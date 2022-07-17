# Hash Table
- Hash tables are used to store key-value pairs.
- They are like arrays, but the keys are not ordered.
- Unlike arrays, hash tables are fast for all of the following operations: finding, adding and removing values.

## Hash Function
- It is a function that takes data of arbitrary size as an input and yields data of fixed size.

- `What makes a good function`?
  - Fast (i.e constant time)
  - Doesn't cluster outputs at specific indices, but distributes uniformly
  - Deterministic (same input yields same output)

- Example
```ts
function hash(input: string, len: number) {
  let total = 0;
  for(let char of input) {
    let value = char.charCodeAt(0) - 96;
    total = (total + value) % len;
  }

  return total;
}
```

## Handle Collision of keys
- Separate Changing
- Linear Probing
- and more

## Big O
| Methods | Time | Space |
| Insertion | O(1) / O(N) | O(1) / O(N) |
| Removal | O(1) / O(N) | O(1) / O(N) |
| Access | O(1) / O(N) | O(1) / O(N) |

```ts
class HashTable {
  keyMap: any[];

  constructor(size: number = 23) {
    this.keyMap = new Array(size);
  }

  _hash(key: string) {
    let total = 0;
    let WEIRD_PRIME = 31;
    for(let i = 0; i < Math.min(key.length, 100) - 1; i++) {
      let value = key[i].charCodeAt(i) - 96;
      total = (total * WEIRD_PRIME + value) % this.keyMap.length;
    }

    return total;
  }

  set<T>(key: string, value: T) {
    let index = this._hash(key);
    if(!this.keyMap[index]) {
      this.keyMap[index] = [];
    }

    // separate chaining
    this.keyMap[index].push([key, value]);

    return index;
  }

  get(key: string) {
    const index = this._hash(key);

    if(!this.keyMap[index]) return undefined;

    const data = this.keyMap[index];
    for(let i = 0; i < data.length - 1; i++) {
      if(data[i][0] === key) return data[i][1]
    }
  }

  loop(cb: Function) {
    for(let i = 0; i < this.keyMap.length - 1; i++) {
      let values = this.keyMap[i];

      if(!values) continue;

      for(let j = 0; j < values.length - 1; j++) {
        cb(values[j]);
      }
    }
  }

  keys() {
    let keysArr = [];

    this.loop((keyValue: any[]) => {
      if(!keysArr.includes(keyValue[0])) {
        keysArr.push(keyValue[0]);
      }
    });

    return keysArr;
  }

  values() {
    let valuesArr = [];

    this.loop((keyValue: any[]) => {
      if(!valuesArr.includes(keyValue[1])) {
        valuesArr.push(keyValue[1]);
      }
    });

    return valuesArr;
  }
}
```