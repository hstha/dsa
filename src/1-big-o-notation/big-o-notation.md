# Big O Notation
- It is a score given to an algorithm which tells how code performs.

## Why it is useful?
- It's important to have a precise vocabulary to talk about how our code performs
- Useful for discussing trade-offs between different approaches
- When our code slows down or crashes, identifying parts of the code that are inefficient can help us find pain points in our applications

## Time Complexity
- We as that an algorithm is O(f(n)) if the number of simple operations the computer has to do is eventually less than a constant times f(n), as n increases

### How to calculate time complexity?
- Count no. of simple operations that computer has to perform.
- Depending on what we count, the number of operations can be as low as x or xn or as high as xn + y.

### Rule of thumbs for calculation of time complexity
- Arithmetic operations are constant
- Variable assignment is constant
- Accessing elements in an array (by index) or object (by key) is constant
- In a loop, the complexity is the length of the loop times the complexity of whatever happens inside of the loop

### Rule of thumbs for reviewing result of time complexity
- Constants don't mater
  - O(2n) === O(n)
  - O(500) === O(1)
  - O(13n^2) === O(n^2)

- Smaller terms don't matter
  - O(n + 10) === O(n)
	- O(1000n + 50) === O(n)
	- O(n^2 + 5n + 8) === O(n^2 + 5n)

### Types of O(f(n))
- could be linear i.e O(f(n)) = n
- could be quadratic i.e O(f(n)) = n^2
- could be constant i.e O(f(n)) = 1
- could be something entirely different!

```js
// always 3 operators independent of n
// O(3) === O(1)
function addUpTo(n) {
    return n * (n + 1) / 2;
}

// 2 operators independent of n and 5 operator dependent of n
// O(5n + 2)
function addUpTo(n) {
    let total = 0;
    for (let i = 1; i <= n; i++) {
        total += i;
    }
    return total;
}

// O(2n) === O(n)
function countUpAndDown(n) {
	for(let i = 0; i < n; i++) {}

	for(let j = n - 1; j >= 0; j--) {}
}

// O(n^2)
function printAllPairs(n) {
	for(let i = 0; i < n; i++) {
		for(let j = 0; j < n; j++) {}
	}
}
```

## Space Complexity
- It means how much additional memory do we need to allocate in order to run the code in our algorithm.
- When input in the algorithm increases ofcourse the total space of the algorithm increases which is not covered by space complexity.
- Space complexity covers auxiliary space complexity which refers to space required by the algorithm, not including space taken up by the inputs.

### Rule of thumbs for calculation of space complexity
- Most primitives (booleans, numbers, undefined, null) are constant space
- String require O(n) space (where n is the string length)
- Reference types are generally O(n), where n is the length (for arrays) or the number of keys (for objects).

```js
// O(1)
function sum(arr) {
	let total = 0;
	for(let i = 0; i < arr.length; i++) {
		total += arr[i];
	}
	return;
}

// O(n + 1) === O(n)
function double(arr) {
	let newArr = [];
	for(let i = 0; i < arr.length; i++) {
		newArr.push(2 * arr[i]);
	}
	return newArr;
}
```

## Logarithms
- A log is inverse of exponential.
  - eg: logx(value) = y === x ^ y = value
- Logarithmic time complexity is great.

### Who cares?
- Certain search algorithms have logarithmic time complexity.
- Efficient sorting algorithms involve logarithms.
- Recursion sometimes involves logarithmic space complexity.

## Summary
- To analyze the performance of an algorithm, we use Big O Notation.
- Big O Notation can give us a high level understanding of the time or space complexity of an algorithm.
- Big O Notation doesn't care about precision, only about general trends (linear? quadratic? constant?).
- The time or space complexity (as measured by Big O) depends only on the algorithm, not the hardware used to run the algorithm.