# Trees

### Trees

Trees are data structures that link nodes in a parent/child relationship, meaning there are nodes that depend on or come off other nodes.

<figure><img src="../.gitbook/assets/image (5).png" alt="" width="295"><figcaption></figcaption></figure>

Trees are formed by a root node (the first node on the tree), and all the nodes that come off that root are called children. The nodes at the bottom of the tree, which have no "descendants", are called leaf nodes. The height of the tree is determined by the number of parent/child connections it has.

Unlike linked lists or arrays, trees are non-linear, meaning when iterating the tree, the program flow can follow different directions within the data structure and hence arrive at different values. In linked lists or arrays, the program can only iterate the data structure from one end to the other, always following the same path.

An important requirement for tree formation is that the only valid connection between nodes is from parent to child. Connections between siblings or from child to parent are not allowed in trees (these types of connections form graphs, a different type of data structure). Another important requirement is that trees must have only one root.

#### Common Uses of Trees

* The DOM model.
* Situation analysis in artificial intelligence.
* File folders in operating systems.

#### Types of Trees

There are many different types of trees. In each type, values may be organized following different patterns that make this data structure more suitable to use when facing different kinds of problems. The most commonly used types of trees are binary trees and heaps.

#### Binary Trees

Binary trees are a type of tree in which each node has a maximum of two children.

<figure><img src="../.gitbook/assets/image (6).png" alt="" width="375"><figcaption></figcaption></figure>

One key situation in which binary trees are really useful is in searching. For searching, a certain type of binary tree is used, called binary search trees (BSTs).

BSTs are just like binary trees but the information within them is ordered in a way that makes them a suitable data structure for searching.

In BST, values are ordered so that each node that descends to the left side of its parent must have a value less than its parent, and each node that descends to the right side of its parent must have a value greater than its parent.

<figure><img src="../.gitbook/assets/image (7).png" alt="" width="213"><figcaption></figcaption></figure>

This order in its values makes this data structure great for searching since at every level of the tree we can identify if the value being looked for is greater or less than the parent node, and from that comparison progressively discard roughly half of the data until we reach our value.

When inserting or deleting values, the algorithm will follow these steps:

* Check if there's a root node.
* If there is, check if the value to add/delete is greater or smaller than the node.
* If it is smaller, check if there is a node to the left and repeat the previous operation. If there's not, add/remove the node in that position.
* If it is greater, check if there is a node to the right and repeat the previous operation. If there's not, add/remove the node in that position.

Searching in BSTs is very similar, only instead of adding/deleting values we check the nodes for equality with the value we're looking for.

#### Implementation of a Binary Search Tree

```javascript
// We create a class for each node within the tree
class Node {
  // Each node has three properties, its value, a pointer that indicates the node to its left and a pointer that indicates the node to its right
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

// We create a class for the BST
class BinarySearchTree {
  // The tree has only one property which is its root node
  constructor() {
    this.root = null;
  }

  // The insert method takes a value as parameter and inserts the value in its corresponding place within the tree
  insert(value) {
    const newNode = new Node(value);
    if (this.root === null) {
      this.root = newNode;
      return this;
    }
    let current = this.root;
    while (true) {
      if (value === current.value) return undefined;
      if (value < current.value) {
        if (current.left === null) {
          current.left = newNode;
          return this;
        }
        current = current.left;
      } else {
        if (current.right === null) {
          current.right = newNode;
          return this;
        }
        current = current.right;
      }
    }
  }

  // The find method takes a value as parameter and iterates through the tree looking for that value
  // If the value is found, it returns the corresponding node and if it's not, it returns undefined
  find(value) {
    if (this.root === null) return false;
    let current = this.root,
      found = false;
    while (current && !found) {
      if (value < current.value) {
        current = current.left;
      } else if (value > current.value) {
        current = current.right;
      } else {
        found = true;
      }
    }
    if (!found) return undefined;
    return current;
  }

  // The contains method takes a value as parameter and returns true if the value is found within the tree
  contains(value) {
    if (this.root === null) return false;
    let current = this.root,
      found = false;
    while (current && !found) {
      if (value < current.value) {
        current = current.left;
      } else if (value > current.value) {
        current = current.right;
      } else {
        return true;
      }
    }
    return false;
  }
}
```

#### Event Loop in JavaScript and How it Uses Data Structures

JavaScript has a concurrency model based on an "event loop". This model is quite different from the model of other languages like C or Java.

#### Stack

Function calls form a stack of frames. A frame encapsulates information such as the context and local variables of a function.

```javascript
function f(b) {
  var a = 12;
  return a + b + 35;
}

function g(x) {
  var m = 4;
  return f(m * x);
}

g(21);
```

When `g` is called, a first frame is created, which contains `g`'s arguments and local variables. When `g` calls `f`, a second frame is created and placed on top of the first, with `f`'s arguments and local variables. When `f` finishes executing, the last frame (in this case `f`) is popped off the stack (leaving only the frame for `g`). When `g` finishes executing, the stack is empty.

#### Heap

Objects are placed in a heap, which, as the name suggests, denotes a large region of memory, mostly without structure or order.

#### Queue

A JavaScript runtime contains a message queue, which is a list of messages to be processed. Each message is associated with a function. When the stack is empty, a message is taken out of the queue and processed. Processing a message involves calling the associated function (thus creating a frame on the stack). The processed message is finished when the stack is empty again.

#### Event Loop

The event loop gets its name by the way it is usually implemented, which generally resembles:

```javascript
while (queue.waitForMessage()) {
  queue.processNextMessage();
}
```

`queue.waitForMessage` waits synchronously for a message if there is none currently.

#### "Run-to-completion"

Each message is processed completely before any other message is processed. This offers some convenient properties when thinking about a program, including the fact that every time a function runs, it cannot be interrupted, and it will run entirely before any other code executes (thus potentially modifying the information the function manipulates). This is different from C, for example, where if a function runs on a thread, it can be stopped at any point to execute code on another thread.

A disadvantage of this model is that if a message takes a long time to complete, the application is unable to process user interactions such as clicks or scrolling. The browser mitigates this disadvantage with the message "a script is taking too long to run". A good practice is to keep the message processing short and, if possible, break a message into several smaller ones.
