# Computer Science Algorithms Fundamentals

#computer-science #algorithms #data-structures #fundamentals #theory

created: 1723292400000
updated: 1724443200000

---

## Overview

Algorithms are step-by-step procedures for solving computational problems. Understanding fundamental algorithms is crucial for computer science and software development. This comprehensive guide covers essential algorithmic concepts, analysis techniques, and common algorithm patterns.

## 🎯 Learning Objectives

By the end of this guide, you should understand:

- Time and space complexity analysis
- Common algorithmic patterns and techniques
- How to choose appropriate algorithms for different problems
- Implementation strategies for fundamental algorithms

## Algorithm Analysis

### Time Complexity (Big O Notation)

Time complexity describes how algorithm runtime scales with input size.

#### Common Time Complexities

**O(1) - Constant Time**

```javascript
function getFirstElement(array) {
  return array[0]; // Always takes same time regardless of array size
}

function hashTableLookup(hashTable, key) {
  return hashTable[key]; // Direct access
}
```

**O(log n) - Logarithmic Time**

```javascript
function binarySearch(sortedArray, target) {
  let left = 0;
  let right = sortedArray.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (sortedArray[mid] === target) {
      return mid;
    } else if (sortedArray[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1; // Not found
}

// Example usage
const numbers = [1, 3, 5, 7, 9, 11, 13, 15];
console.log(binarySearch(numbers, 7)); // Returns index 3
```

**O(n) - Linear Time**

```javascript
function linearSearch(array, target) {
  for (let i = 0; i < array.length; i++) {
    if (array[i] === target) {
      return i;
    }
  }
  return -1;
}

function findMaximum(numbers) {
  let max = numbers[0];
  for (let i = 1; i < numbers.length; i++) {
    if (numbers[i] > max) {
      max = numbers[i];
    }
  }
  return max;
}
```

**O(n log n) - Linearithmic Time**

```javascript
function mergeSort(array) {
  if (array.length <= 1) {
    return array;
  }

  const mid = Math.floor(array.length / 2);
  const left = mergeSort(array.slice(0, mid));
  const right = mergeSort(array.slice(mid));

  return merge(left, right);
}

function merge(left, right) {
  const result = [];
  let leftIndex = 0;
  let rightIndex = 0;

  while (leftIndex < left.length && rightIndex < right.length) {
    if (left[leftIndex] < right[rightIndex]) {
      result.push(left[leftIndex]);
      leftIndex++;
    } else {
      result.push(right[rightIndex]);
      rightIndex++;
    }
  }

  return result.concat(left.slice(leftIndex)).concat(right.slice(rightIndex));
}
```

**O(n²) - Quadratic Time**

```javascript
function bubbleSort(array) {
  const n = array.length;
  for (let i = 0; i < n - 1; i++) {
    for (let j = 0; j < n - i - 1; j++) {
      if (array[j] > array[j + 1]) {
        // Swap elements
        [array[j], array[j + 1]] = [array[j + 1], array[j]];
      }
    }
  }
  return array;
}

function findAllPairs(array) {
  const pairs = [];
  for (let i = 0; i < array.length; i++) {
    for (let j = i + 1; j < array.length; j++) {
      pairs.push([array[i], array[j]]);
    }
  }
  return pairs;
}
```

### Space Complexity

Space complexity measures memory usage relative to input size.

```javascript
// O(1) Space - Constant
function sumArray(numbers) {
  let sum = 0; // Only uses one variable
  for (let num of numbers) {
    sum += num;
  }
  return sum;
}

// O(n) Space - Linear
function reverseArray(array) {
  const reversed = []; // Creates new array of same size
  for (let i = array.length - 1; i >= 0; i--) {
    reversed.push(array[i]);
  }
  return reversed;
}

// O(log n) Space - Logarithmic (recursive calls)
function binarySearchRecursive(
  array,
  target,
  left = 0,
  right = array.length - 1
) {
  if (left > right) return -1;

  const mid = Math.floor((left + right) / 2);

  if (array[mid] === target) return mid;
  else if (array[mid] < target)
    return binarySearchRecursive(array, target, mid + 1, right);
  else return binarySearchRecursive(array, target, left, mid - 1);
}
```

## Fundamental Sorting Algorithms

### Bubble Sort

Simple but inefficient sorting algorithm.

```javascript
function bubbleSort(arr) {
  const n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    let swapped = false;

    for (let j = 0; j < n - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // Swap elements
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
        swapped = true;
      }
    }

    // If no swapping occurred, array is sorted
    if (!swapped) break;
  }

  return arr;
}

// Time Complexity: O(n²)
// Space Complexity: O(1)
```

### Selection Sort

Finds minimum element and places it at the beginning.

```javascript
function selectionSort(arr) {
  const n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    let minIndex = i;

    // Find minimum element in remaining array
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }

    // Swap minimum with first element
    if (minIndex !== i) {
      [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
    }
  }

  return arr;
}

// Time Complexity: O(n²)
// Space Complexity: O(1)
```

### Insertion Sort

Builds sorted array one element at a time.

```javascript
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    const key = arr[i];
    let j = i - 1;

    // Move elements greater than key one position ahead
    while (j >= 0 && arr[j] > key) {
      arr[j + 1] = arr[j];
      j--;
    }

    arr[j + 1] = key;
  }

  return arr;
}

// Time Complexity: O(n²) worst case, O(n) best case
// Space Complexity: O(1)
```

### Quick Sort

Divide-and-conquer algorithm using a pivot element.

```javascript
function quickSort(arr, low = 0, high = arr.length - 1) {
  if (low < high) {
    const pivotIndex = partition(arr, low, high);

    quickSort(arr, low, pivotIndex - 1);
    quickSort(arr, pivotIndex + 1, high);
  }

  return arr;
}

function partition(arr, low, high) {
  const pivot = arr[high];
  let i = low - 1;

  for (let j = low; j < high; j++) {
    if (arr[j] < pivot) {
      i++;
      [arr[i], arr[j]] = [arr[j], arr[i]];
    }
  }

  [arr[i + 1], arr[high]] = [arr[high], arr[i + 1]];
  return i + 1;
}

// Time Complexity: O(n log n) average, O(n²) worst case
// Space Complexity: O(log n)
```

## Searching Algorithms

### Linear Search

Check each element sequentially.

```javascript
function linearSearch(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      return i; // Return index
    }
  }
  return -1; // Not found
}

// With additional information
function linearSearchDetailed(arr, target) {
  let comparisons = 0;

  for (let i = 0; i < arr.length; i++) {
    comparisons++;
    if (arr[i] === target) {
      return { found: true, index: i, comparisons };
    }
  }

  return { found: false, index: -1, comparisons };
}
```

### Binary Search

Efficient search on sorted arrays.

```javascript
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid;
    } else if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1;
}

// Recursive version
function binarySearchRecursive(arr, target, left = 0, right = arr.length - 1) {
  if (left > right) return -1;

  const mid = Math.floor((left + right) / 2);

  if (arr[mid] === target) return mid;
  else if (arr[mid] < target)
    return binarySearchRecursive(arr, target, mid + 1, right);
  else return binarySearchRecursive(arr, target, left, mid - 1);
}
```

## Basic Data Structures

### Stack (LIFO - Last In, First Out)

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(element) {
    this.items.push(element);
  }

  pop() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items.pop();
  }

  peek() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items[this.items.length - 1];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }

  clear() {
    this.items = [];
  }

  toString() {
    return this.items.toString();
  }
}

// Usage example
const stack = new Stack();
stack.push(1);
stack.push(2);
stack.push(3);
console.log(stack.peek()); // 3
console.log(stack.pop()); // 3
console.log(stack.size()); // 2
```

### Queue (FIFO - First In, First Out)

```javascript
class Queue {
  constructor() {
    this.items = [];
  }

  enqueue(element) {
    this.items.push(element);
  }

  dequeue() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items.shift();
  }

  front() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items[0];
  }

  rear() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items[this.items.length - 1];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }

  clear() {
    this.items = [];
  }
}

// Usage example
const queue = new Queue();
queue.enqueue("A");
queue.enqueue("B");
queue.enqueue("C");
console.log(queue.front()); // 'A'
console.log(queue.dequeue()); // 'A'
console.log(queue.size()); // 2
```

### Linked List

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
    this.size = 0;
  }

  append(data) {
    const newNode = new Node(data);

    if (!this.head) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next) {
        current = current.next;
      }
      current.next = newNode;
    }

    this.size++;
  }

  prepend(data) {
    const newNode = new Node(data);
    newNode.next = this.head;
    this.head = newNode;
    this.size++;
  }

  delete(data) {
    if (!this.head) return false;

    if (this.head.data === data) {
      this.head = this.head.next;
      this.size--;
      return true;
    }

    let current = this.head;
    while (current.next && current.next.data !== data) {
      current = current.next;
    }

    if (current.next) {
      current.next = current.next.next;
      this.size--;
      return true;
    }

    return false;
  }

  find(data) {
    let current = this.head;
    let index = 0;

    while (current) {
      if (current.data === data) {
        return index;
      }
      current = current.next;
      index++;
    }

    return -1;
  }

  toArray() {
    const result = [];
    let current = this.head;

    while (current) {
      result.push(current.data);
      current = current.next;
    }

    return result;
  }
}
```

## Dynamic Programming

### Fibonacci Sequence

```javascript
// Naive recursive approach - O(2^n)
function fibonacciNaive(n) {
  if (n <= 1) return n;
  return fibonacciNaive(n - 1) + fibonacciNaive(n - 2);
}

// Memoization approach - O(n)
function fibonacciMemo(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;

  memo[n] = fibonacciMemo(n - 1, memo) + fibonacciMemo(n - 2, memo);
  return memo[n];
}

// Bottom-up approach - O(n)
function fibonacciDP(n) {
  if (n <= 1) return n;

  const dp = [0, 1];
  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }

  return dp[n];
}

// Space-optimized approach - O(1) space
function fibonacciOptimized(n) {
  if (n <= 1) return n;

  let prev = 0;
  let curr = 1;

  for (let i = 2; i <= n; i++) {
    const temp = curr;
    curr = prev + curr;
    prev = temp;
  }

  return curr;
}
```

## Algorithm Design Patterns

### Divide and Conquer

Break problem into smaller subproblems.

```javascript
// Maximum subarray problem
function maxSubarray(arr, left = 0, right = arr.length - 1) {
  if (left === right) {
    return arr[left];
  }

  const mid = Math.floor((left + right) / 2);

  // Find max in left and right halves
  const leftMax = maxSubarray(arr, left, mid);
  const rightMax = maxSubarray(arr, mid + 1, right);

  // Find max crossing the middle
  let leftSum = -Infinity;
  let sum = 0;
  for (let i = mid; i >= left; i--) {
    sum += arr[i];
    leftSum = Math.max(leftSum, sum);
  }

  let rightSum = -Infinity;
  sum = 0;
  for (let i = mid + 1; i <= right; i++) {
    sum += arr[i];
    rightSum = Math.max(rightSum, sum);
  }

  const crossMax = leftSum + rightSum;

  return Math.max(leftMax, rightMax, crossMax);
}
```

### Greedy Algorithms

Make locally optimal choices.

```javascript
// Activity selection problem
function activitySelection(activities) {
  // Sort by finish time
  activities.sort((a, b) => a.finish - b.finish);

  const selected = [activities[0]];
  let lastFinishTime = activities[0].finish;

  for (let i = 1; i < activities.length; i++) {
    if (activities[i].start >= lastFinishTime) {
      selected.push(activities[i]);
      lastFinishTime = activities[i].finish;
    }
  }

  return selected;
}

// Coin change (greedy - only works for certain coin systems)
function coinChangeGreedy(amount, coins) {
  coins.sort((a, b) => b - a); // Sort in descending order

  const result = [];
  for (const coin of coins) {
    while (amount >= coin) {
      result.push(coin);
      amount -= coin;
    }
  }

  return amount === 0 ? result : null; // null if no solution
}
```

## Practical Applications

### String Algorithms

```javascript
// Pattern matching (naive approach)
function naiveStringMatch(text, pattern) {
  const matches = [];

  for (let i = 0; i <= text.length - pattern.length; i++) {
    let j;
    for (j = 0; j < pattern.length; j++) {
      if (text[i + j] !== pattern[j]) {
        break;
      }
    }

    if (j === pattern.length) {
      matches.push(i);
    }
  }

  return matches;
}

// Palindrome check
function isPalindrome(str) {
  const cleaned = str.toLowerCase().replace(/[^a-z0-9]/g, "");
  let left = 0;
  let right = cleaned.length - 1;

  while (left < right) {
    if (cleaned[left] !== cleaned[right]) {
      return false;
    }
    left++;
    right--;
  }

  return true;
}
```

### Graph Algorithms Basics

```javascript
// Graph representation using adjacency list
class Graph {
  constructor() {
    this.vertices = {};
  }

  addVertex(vertex) {
    if (!this.vertices[vertex]) {
      this.vertices[vertex] = [];
    }
  }

  addEdge(vertex1, vertex2) {
    this.addVertex(vertex1);
    this.addVertex(vertex2);

    this.vertices[vertex1].push(vertex2);
    this.vertices[vertex2].push(vertex1); // For undirected graph
  }

  // Depth-First Search
  dfs(startVertex, visited = new Set()) {
    visited.add(startVertex);
    console.log(startVertex);

    for (const neighbor of this.vertices[startVertex] || []) {
      if (!visited.has(neighbor)) {
        this.dfs(neighbor, visited);
      }
    }
  }

  // Breadth-First Search
  bfs(startVertex) {
    const visited = new Set();
    const queue = [startVertex];
    visited.add(startVertex);

    while (queue.length > 0) {
      const vertex = queue.shift();
      console.log(vertex);

      for (const neighbor of this.vertices[vertex] || []) {
        if (!visited.has(neighbor)) {
          visited.add(neighbor);
          queue.push(neighbor);
        }
      }
    }
  }
}
```

This comprehensive guide covers fundamental algorithms and data structures essential for computer science understanding and programming interviews.
