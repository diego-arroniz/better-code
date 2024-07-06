# Stacks

### Stacks

We are all familiar with the Undo option, which is present in almost all applications. Have you ever wondered how it works? The idea: you store the previous states of your work (which are limited to a specific number) in memory in such an order that the last one appears first. This cannot be done using arrays alone. This is where the Stack comes in handy.

A real-life example of using a Stack could be a stack of books placed in a vertical order. To get the book that is somewhere in the middle, you will need to remove all the books that are above it. This is how the LIFO (Last In First Out) method works.

Below you can find an image of a stack containing 3 data elements (1, 2, and 3), where 3 is on top and will be removed first:

<figure><img src="../.gitbook/assets/image (3).png" alt="" width="375"><figcaption></figcaption></figure>

#### Basic Stack Operations

* **Push** — Inserts an element at the top.
* **Pop** — Returns the top element after removing it from the stack.
* **Peek** — Returns the element at the top without removing it from the stack.
* **Size** — Returns the size of the stack.

```javascript
class Stack {
  constructor() {
    this.stack = [];
  }

  push(element) {
    this.stack.push(element);
    return this.stack;
  }

  pop() {
    return this.stack.pop();
  }

  peek() {
    return this.stack[this.stack.length - 1];
  }

  size() {
    return this.stack.length;
  }

  print() {
    console.log(this.stack);
  }
}

const stack = new Stack();
console.log(stack.size()); // 0
console.log(stack.push('John Cena')); // ['John Cena']
console.log(stack.push('The Rock')); // ['John Cena', 'The Rock']
console.log(stack.size()); // 2
stack.print(); // ['John Cena', 'The Rock']
console.log(stack.peek()); // 'The Rock'
console.log(stack.pop()); // 'The Rock'
console.log(stack.peek()); // 'John Cena'
```
