# Functional Programming

## Functional Programming

JavaScript is a multi-paradigm language and can be written following different programming paradigms. A programming paradigm is essentially a set of rules to follow when writing code.

Because it is a sub-paradigm of the declarative paradigm, it affects the way you write functional code. Generally, it leads to less code because JavaScript already has many built-in functions you normally need. This is one of the reasons people like functional code.

Functional programming can be simply explained by following these two rules in your code:

1. Design your software using pure and isolated functions.
2. Avoid mutability and side effects.

### 1. Design Your Software Using Pure and Isolated Functions

#### Pure Functions

The same input always gives the same output (idempotence) and has no side effects.

An idempotent function is one that, when its results are applied to that function again, does not produce a different result.

Side effects occur when your code interacts with (reads or writes) mutable external state.

Mutable external state is literally anything outside the function that would change data in your program. Setting a function? Setting a boolean in an object? Deleting properties from an object? All changes in state outside your function.

#### Isolated Functions

They do not depend on the program state, which includes global variables that are subject to changes.

Everything you need should be passed to the function as an argument. This makes your dependencies (things the function needs to do its job) much clearer to see and more detectable.

#### Reusability Through Higher-Order Functions

Functions that can be assigned to a variable, passed to another function, or returned from another function as any other normal value are called first-class functions.

In JavaScript, all functions are first-class functions. Functions that have first-class status allow us to create higher-order functions.

A higher-order function is a function that takes another function as an argument, returns a function, or does both! You can use higher-order functions to stop repeating code.

The array functions included in JavaScript `.map`, `.reduce`, and `.filter` accept a function. They are excellent examples of higher-order functions, as they iterate over an array and call the function they received for each element in the array.

### 2. Avoid Mutability and Side Effects

Basically, it all comes down to this: don't change things! Once you've done so, it's immutable (it won't change anymore).

If something has to change in your data structure, make the changes in a copy.

```javascript
const ages = [12, 32, 32, 53];
const newAges = ages.map(function (age) {
  if (age === 12) {
    return 20;
  } else {
    return age;
  }
});
```

If we cannot change the global state of the variables, then we must ensure:

* Declare function arguments: any calculation within a function depends only on the arguments and not on any global object or variable.
* Do not modify a variable or object: create new variables and objects and return them if necessary, from a function.

#### Make Your Code Referentially Transparent

When you follow the rule of never changing the state, your code becomes referentially transparent. That is, your function calls can be replaced with the values they represent, without affecting the result.

As a simple example to verify if your code is referentially transparent, look at the following code snippet:

```javascript
javascriptCopy codeconst greetAuthor = function() {
  return 'Hello Kealan';
};
```

You should be able to simply swap that function call with the string it returns and not have any problems.

Functional programming with referentially transparent expressions makes you start thinking about your code differently if you're used to object-oriented programming.

#### But, Why?

Because instead of objects and mutable states in your code, you start having pure functions, with no state changes. You clearly understand what you expect your function to return (since it never changes, when it normally could return different data types depending on the state outside the function).

It can help you better understand the flow, understand what a function is doing just by scanning it, and be more rigorous with each function's responsibilities to create better-decoupled systems.

### More Features of Functional Programming

#### Recursion in Functional Programming

In JavaScript, a function can call itself.

```javascript
javascriptCopy codefunction recur(start, end) {
  if (start === end) {
    console.log(end);
    return;
  } else {
    console.log(start);
    return recur(start + 1, end);
  }
}

recur(1, 10);
// 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
```

#### Why Use Recursion?

Recursion allows us to stop mutating state variables, to begin with.

There are also certain data structures (tree structures) that are more efficient when solved with recursion. They usually require less code, so some developers like the ease of reading recursion.

#### Currying in Functional Programming

Currying is another tool widely used in functional code. The arity of a function refers to how many arguments it receives.

```javascript
javascriptCopy code// Let's look at arity
function arity2(arg1, arg2) {}             // Function has an arity of 2
function arity0() {}                       // Function has an arity of 0
function arity4(arg1, arg2, arg3, arg4) {} // Function has an arity of 4
```

Currying a function converts this function that has an arity of more than 1 into a function of arity 1. It does this by returning an inner function to take the next argument. Here is an example:

```javascript
javascriptCopy codefunction sum(firstNum, secondNum) {
  return firstNum + secondNum;
}

// Currying this function
function currySum(firstNum) {
  return function(secondNum) {
    return firstNum + secondNum;
  };
}
```

Essentially, it restructures a function to take one argument, but then returns another function to take the next argument, as many times as necessary.

#### Why Use Currying?

The big benefit of currying is when you need to reuse the same function multiple times, but only change one (or fewer) of the parameters. Then you can save the first call to the function, something like this:

```javascript
javascriptCopy codefunction currySum(firstNum) {
  return function(secondNum) {
    return firstNum + secondNum;
  };
}

let sum10 = currySum(10);
sum10(2); // Returns 12

let sum20 = currySum(20);
sum20(2); // Returns 22
```

Currying can also make your code easier to refactor. You don't have to change multiple places where you're passing the wrong function arguments, just the place where you bound the first function call to the wrong argument.

It's also useful if you can't provide all the arguments to a function at once. You can return the first function to call the inner function when you have all the arguments later.

#### Partial Application in Functional Programming

Similarly, partial application means you apply some arguments to a function at a time and return another function that applies more arguments. This is the best example I found in the MDN documentation:

```javascript
javascriptCopy codeconst module = {
  height: 42,
  calculateHeight: function(height) {
    return this.height + height;
  }
};

const isolatedCalculateHeight = module.calculateHeight;
console.log(isolatedCalculateHeight(32)); // The function is invoked from the global scope
// Outputs: NaN
// Outputs NaN because this.height is undefined (in the window scope)
// undefined + 32 which returns NaN

const boundCalculateHeight = isolatedCalculateHeight.bind(module);
console.log(boundCalculateHeight(32));
// Expected output: 74
```

`bind` is the best example of partial application. Why?

Because we return an inner function that is assigned to `boundCalculateHeight` which is called, with this scope set correctly and a new argument passed later. We do not assign all arguments at once but return a function to accept the rest of the arguments.

#### Why Use Partial Application?

You can use partial application whenever you can't pass all its arguments at once but can return higher-order functions to deal with the rest of the arguments.

#### Function Composition in Functional Programming

Function composition allows us to take two or more functions and turn them into a single function that does exactly what the two (or more) functions do.

```javascript
javascriptCopy code// If we have these two functions
function add10(num) {
  return num + 10;
}
function add100(num) {
  return num + 100;
}

// We can compose these two into the following =>
function composed(num) {
  return add10(add100(num));
}

composed(1); // Returns 111
```

You can take this further and create functions to compose any number of functions of multiple arities together if needed.

#### Why Use Function Composition?

Composition allows you to structure your code from reusable functions to stop repeating yourself. You can start treating functions as small building blocks that you can combine to achieve a more complicated result.

These then become the "units" or the computational power in your programs. They are many small functions that work generically, all composed into larger functions to do the "real" work.

It's a powerful way to design your code and prevents you from creating huge functions that are copied and pasted with small differences between them.

***

**Source:** [What is Functional Programming - A Beginner's JavaScript Guide](https://www.freecodecamp.org/espanol/news/que-es-la-programacion-funcional-una-guia-de-javascript-para-principiantes/)
