# Decorator

#### Decorator

The Decorator pattern helps you add new functions to existing objects simply by wrapping them inside a new object. It's similar to how you can wrap an already wrapped gift box with new wrapping paper as many times as you want: each wrapping allows you to add as many functions as you want, so it's very flexible.

From a technical point of view, there is no inheritance, so there is greater freedom in designing the business logic.

In the following example, you'll see how the Decorator pattern helps add more functions to a standard `Customer` class:

```javascript
javascriptCopy codefunction Customer(name, age) { 
   this.name = name; 
   this.age = age;

   this.printInfo = function() { 
       console.log("Customer:\nName: " + this.name + " | Age: " + this.age);
   };
}

function DecoratedCustomer(customer, location) { 
   this.customer = customer; 
   this.name = customer.name; 
   this.age = customer.age; 
   this.location = location;

   this.printInfo = function() { 
       console.log("Decorated Customer:\nName: " + this.name + " | Age: " + this.age + " | Location: " + this.location);
   };
}

function run() { 
   let customer = new Customer("John", 25);
   customer.printInfo();
   // Output: 
   // Customer: 
   // Name : John | Age: 25 

   let decoratedCustomer = new DecoratedCustomer(customer, "FL");
   decoratedCustomer.printInfo();
   // Output: 
   // Decorated Customer: 
   // Name : John | Age: 25 | Location: FL 
}

run();
```

The drawbacks of this pattern include the high complexity of the code since there is no standard defined pattern for adding new functions via decorators. You might end up with a lot of non-uniform and/or similar decorators at the end of your software development lifecycle.

If you are not careful when designing the decorators, you may end up designing decorators that logically depend on each other. If this is not resolved, removing or restructuring the decorators later can wreak havoc on the stability of your application.
