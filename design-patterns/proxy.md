# Proxy

#### Proxy

The Proxy pattern helps you substitute one object for another. In other words, proxy objects can take the place of real objects (of which they are a proxy) and control access to the object. These proxy objects can be used to perform some actions before or after passing an invocation request to the real object.

In the following example, you'll see how access to a database instance is controlled via a proxy that performs some basic validation checks on requests before allowing them to pass:

```javascript
function DatabaseHandler() { 
   const data = {};

   this.set = function(key, val) { 
       data[key] = val; 
   };
   this.get = function(key) { 
       return data[key]; 
   };
   this.remove = function(key) { 
       data[key] = null; 
   };
}

function DatabaseProxy(databaseInstance) { 
   this.set = function(key, val) { 
       if (key === "") { 
           console.log("Invalid input"); 
           return; 
       }

       if (val === undefined) { 
           console.log("Setting value to undefined not allowed!"); 
           return; 
       }

       databaseInstance.set(key, val); 
   };

   this.get = function(key) { 
       if (databaseInstance.get(key) === null) { 
           console.log("Element deleted"); 
       }

       if (databaseInstance.get(key) === undefined) { 
           console.log("Element not created"); 
       }

       return databaseInstance.get(key); 
   };

   this.remove = function(key) { 
       if (databaseInstance.get(key) === undefined) { 
           console.log("Element not added"); 
           return; 
       }

       if (databaseInstance.get(key) === null) { 
           console.log("Element removed already"); 
           return; 
       }

       return databaseInstance.remove(key); 
   };
}

function run() { 
   let databaseInstance = new DatabaseHandler();
   databaseInstance.set("foo", "bar");
   databaseInstance.set("foo", undefined);
   console.log("#1: " + databaseInstance.get("foo"));
   // #1: undefined

   console.log("#2: " + databaseInstance.get("baz"));
   // #2: undefined

   databaseInstance.set("", "something");
   databaseInstance.remove("foo");
   console.log("#3: " + databaseInstance.get("foo"));
   // #3: null

   databaseInstance.remove("foo");
   databaseInstance.remove("baz");

   databaseInstance = new DatabaseHandler();
   let proxy = new DatabaseProxy(databaseInstance);

   proxy.set("foo", "bar");
   proxy.set("foo", undefined);
   // Proxy jumps in: 
   // Output: Setting value to undefined not allowed! 

   console.log("#1: " + proxy.get("foo"));
   // Original value is retained: 
   // Output: #1: bar 

   console.log("#2: " + proxy.get("baz"));
   // Proxy jumps in again 
   // Output: 
   // Element not created 
   // #2: undefined 

   proxy.set("", "something");
   // Proxy jumps in again 
   // Output: Invalid input 

   proxy.remove("foo");
   console.log("#3: " + proxy.get("foo"));
   // Proxy jumps in again 
   // Output: 
   // Element deleted 
   // #3: null 

   proxy.remove("foo");
   // Proxy output: Element removed already 
   proxy.remove("baz");
   // Proxy output: Element not added 
}

run();
```

This design pattern is commonly used across the industry and helps to easily implement pre- and post-execution operations. However, like any other design pattern, it also adds complexity to your code base, so try not to use it if you don't really need it.

Additionally, since an additional object is involved in making calls to your main object, there can be some latency due to the added processing operations. Optimizing the performance of your main object now also involves optimizing the performance of your proxy methods.
