# Queues

### Queues

Similar to the Stack, the Queue is another linear data structure that stores elements sequentially. The only significant difference between the Stack and the Queue is that instead of using the LIFO method, the Queue implements the FIFO (First In First Out) method.

A perfect real-life example of a Queue: a line of people waiting at a ticket counter. If a new person arrives, they will form at the end of the line, not at the beginning — and the person at the beginning of the line will be the first to get a ticket and, therefore, the first to leave the line.

Below is an image of a Queue containing four data elements (1, 2, 3, and 4), where 1 is at the beginning and will be removed first:

#### Basic Queue Operations

* **Enqueue** — Inserts an element at the end of the queue.
* **Dequeue** — Removes an element from the beginning of the queue.
* **Peek** — Returns the element at the top without removing it from the stack.
* **Size** — Returns the size of the stack.
* **isEmpty** — Returns true if the queue is empty.

```javascript
class Queue {
  constructor() {
    this.queue = [];
  }

  enqueue(element) {
    this.queue.push(element);
    return this.queue;
  }

  dequeue() {
    return this.queue.shift();
  }

  peek() {
    return this.queue[0];
  }

  size() {
    return this.queue.length;
  }

  isEmpty() {
    return this.queue.length === 0;
  }

  print() {
    return this.queue;
  }
}

const queue = new Queue();
console.log(queue.enqueue('The Rock')); // ['The Rock']
console.log(queue.enqueue('John Cena')); // ['The Rock', 'John Cena']
console.log(queue.enqueue('Stone Cold Steve Austin')); // ['The Rock', 'John Cena', 'Stone Cold Steve Austin']
console.log(queue.dequeue()); // 'The Rock'
console.log(queue.peek()); // 'John Cena'
console.log(queue.isEmpty()); // false
console.log(queue.print()); // ['John Cena', 'Stone Cold Steve Austin']
```
