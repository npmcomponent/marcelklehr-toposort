*This repository is a mirror of the [component](http://component.io) module [marcelklehr/toposort](http://github.com/marcelklehr/toposort). It has been modified to work with NPM+Browserify. You can install it using the command `npm install npmcomponent/marcelklehr-toposort`. Please do not open issues or send pull requests against this repo. If you have issues with this repo, report it to [npmcomponent](https://github.com/airportyh/npmcomponent).*
# Toposort

Sort directed acyclic graphs

[![Build Status](https://travis-ci.org/marcelklehr/toposort.png)](https://travis-ci.org/marcelklehr/toposort)

## Installation

`npm install toposort` or `component install marcelklehr/toposort`  

then in your code:

```js
toposort = require('toposort')
```

## Usage
We want to sort the following graph.

![graph](https://raw.githubusercontent.com/marcelklehr/toposort/master/graph.jpg)

```js
// First, we define our edges.
var graph = [
  ['put on your shoes', 'tie your shoes']
, ['put on your shirt', 'put on your jacket']
, ['put on your shorts', 'put on your jacket']
, ['put on your shorts', 'put on your shoes']
]


// Now, sort the vertices topologically, to reveal a legal execution order.
toposort(graph)
// [ 'put on your shirt'
// , 'put on your shorts'
// , 'put on your jacket'
// , 'put on your shoes'
// , 'tie your shoes' ]
```

(Note that there is no defined order for graph parts that are not connected
 -- you could also put on your jacket after having tied your shoes...)

### Sorting dependencies
It is usually more convenient to specify *dependencies* instead of "sequences".
```js
// This time, edges represent dependencies.
var graph = [
  ['tie your shoes', 'put on your shoes']
, ['put on your jacket', 'put on your shirt']
, ['put on your shoes', 'put on your shorts']
, ['put on your jacket', 'put on your shorts']
]

toposort(graph) 
// [ 'tie your shoes'
// , 'put on your shoes'
// , 'put on your jacket'
// , 'put on your shirt'
// , 'put on your shorts' ]

// Now, reversing the list will reveal a legal execution order.
toposort(graph).reverse() 
// [ 'put on your shorts'
// , 'put on your shirt'
// , 'put on your jacket'
// , 'put on your shoes'
// , 'tie your shoes' ]
```

## API

### toposort(edges)

+ edges {Array} An array of directed edges describing a graph. An edge looks like this: `[node1, node2]` (vertices needn't be strings but can be of any type).

Returns: {Array} a list of vertices, sorted from "start" to "end"

### toposort.array(nodes, edges)

+ nodes {Array} An array of nodes
+ edges {Array} An array of directed edges. You don't need to mention all `nodes` here.

This is a convenience method that allows you to define nodes that may or may not be connected to any other nodes. The ordering of unconnected nodes is not defined.

Returns: {Array} a list of vertices, sorted from "start" to "end"

## Tests

Run the tests with `node test.js`.

## Legal

MIT License