# Singleton

#### Singleton

The Singleton pattern is one of the most used design patterns in the software development industry. The problem it aims to solve is maintaining a single instance of a class. This can be useful when instantiating objects that consume many resources, such as database handlers.

Here's how you can implement it in JavaScript:

```javascript
function SingletonFoo() { 
   let fooInstance = null; 
   let count = 0; 

   function printCount() { 
       console.log("Number of instances: " + count); 
   } 

   function init() { 
       count++; 
       return {}; 
   } 

   function createInstance() { 
       if (fooInstance == null) { 
           fooInstance = init(); 
       } 
       return fooInstance; 
   } 

   function closeInstance() { 
       count--; 
       fooInstance = null; 
   } 

   return { 
       initialize: createInstance, 
       close: closeInstance, 
       printCount: printCount 
   } 
} 

let foo = SingletonFoo(); 

foo.printCount(); // Prints 0 
foo.initialize(); 
foo.printCount(); // Prints 1 
foo.initialize(); 
foo.printCount(); // Still prints 1 
foo.close(); 
foo.printCount(); // Prints 0
```

While it serves its purpose well, the Singleton pattern is known for making debugging difficult, as it masks dependencies and controls access to the initialization or destruction of instances of a class.
