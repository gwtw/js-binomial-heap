# js-binomial-heap  [![NPM version](https://img.shields.io/npm/v/@tyriar/binomial-heap.svg?style=flat)](https://www.npmjs.org/package/@tyriar/binomial-heap)

[![Build Status](http://img.shields.io/travis/Tyriar/js-binomial-heap.svg?style=flat)](http://travis-ci.org/Tyriar/js-binomial-heap) [![Coverage Status](https://img.shields.io/coveralls/Tyriar/js-binomial-heap.svg?branch=master&service=github)](https://coveralls.io/github/Tyriar/js-binomial-heap?branch=master)

A JavaScript implementation of the [binomial heap](http://www.growingwiththeweb.com/2014/01/binomial-heap.html) data structure.

![](http://www.growingwiththeweb.com/images/2014/01/19/binomial-heap.svg)

## Features

- 100% test coverage
- Supports all common heap operations\*
- Store keys with optional associated values
- Optional custom compare function that can utilize both key and value to give full control over the order of the data

\* except [delete](https://github.com/Tyriar/js-binomial-heap/issues/5) and [decrease key](https://github.com/Tyriar/js-binomial-heap/issues/6)

## Install

```bash
npm install --save @tyriar/binomial-heap
```

## Usage

```javascript
// Import npm module
var BinomialHeap = require('@tyriar/binomial-heap';

// Construct BinomialHeap
var heap = new BinomialHeap();
// Insert keys only
heap.insert(3);
heap.insert(7);
// Insert keys and values
heap.insert(8, {foo: 'bar'});
heap.insert(1, {foo: 'baz'});

// Extract all nodes in order
while (!heap.isEmpty()) {
  var node = heap.extractMinimum();
  console.log('key: ' + node.key + ', value: ' + node.value);
}
// > key: 1, value: [object Object]
// > key: 3, value: undefined
// > key: 7, value: undefined
// > key: 8, value: [object Object]

// Construct custom compare BinomialHeap
heap = new BinomialHeap(function (a, b) {
  return (a.key + a.value).localeCompare(b.key + b.value);
});
heap.insert('2', 'B');
heap.insert('1', 'a');
heap.insert('1', 'A');
heap.insert('2', 'b');

// Extract all nodes in order
while (!heap.isEmpty()) {
  var node = heap.extractMinimum();
  console.log('key: ' + node.key + ', value: ' + node.value);
}
// > key: 1, value: a
// > key: 1, value: A
// > key: 2, value: b
// > key: 2, value: B
```

## Operation time complexity

| Operation      | Complexity |
| -------------- | ---------- |
| clear          | Θ(1)       |
| extractMinimum | Θ(log n)   |
| findMinimum    | O(log n)\* |
| insert         | O(log n)   |
| isEmpty        | Θ(1)       |
| size           | Θ(1)       |
| union          | Θ(log n)   |

\* amortized

## API

### BinomialHeap

Creates a binomial heap.

**Parameters**

-   `customCompare` **function** An optional custom node comparison
    function.

#### clear

Clears the heap's data, making it an empty heap.

#### extractMinimum

Extracts and returns the minimum node from the heap.

Returns **Node** node The heap's minimum node or undefined if the heap is
empty.

#### findMinimum

Returns the minimum node from the heap.

Returns **Node** node The heap's minimum node or undefined if the heap is
empty.

#### insert

Inserts a new key-value pair into the heap.

**Parameters**

-   `key` **Object** The key to insert.
-   `value` **Object** The value to insert.

Returns **Node** node The inserted node.

#### isEmpty

Returns **boolean** Whether the heap is empty.

#### size

Returns **number** The size of the heap.

#### union

Joins another heap to this one.

**Parameters**

-   `otherHeap` **BinomialHeap** The other heap.
-   `heap`

### Node

Creates a Binomial Heap node.

**Parameters**

-   `key` **Object** The key of the new node.
-   `value` **Object** The value of the new node.
