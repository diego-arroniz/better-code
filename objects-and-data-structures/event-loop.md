# Event Loop

#### Event Loop in JavaScript and How it Uses Data Structures

JavaScript has a concurrency model based on an "event loop". This model is quite different from the model of other languages like C or Java.

<figure><img src="../.gitbook/assets/image (27).png" alt="" width="173"><figcaption></figcaption></figure>

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
