# Factory

#### Factory

The Factory method is also one of the most popular design patterns. The problem the Factory method aims to solve is creating objects without using the conventional constructor. Instead, it takes the configuration (or description) of the object you want and returns the newly created object.

Here's how you can implement it in JavaScript:

```javascript
function Factory() { 
   this.createDog = function (breed) { 
       let dog; 

       if (breed === "labrador") { 
           dog = new Labrador(); 
       } else if (breed === "bulldog") { 
           dog = new Bulldog(); 
       } else if (breed === "golden retriever") { 
           dog = new GoldenRetriever(); 
       } else if (breed === "german shepherd") { 
           dog = new GermanShepherd(); 
       } 

       dog.breed = breed; 
       dog.printInfo = function () { 
           console.log("Breed: " + dog.breed + "\nShedding Level (out of 5): " + dog.sheddingLevel + "\nCoat Length: " + dog.coatLength + "\nCoat Type: " + dog.coatType); 
       }; 

       return dog; 
   }; 
} 

function Labrador() { 
   this.sheddingLevel = 4; 
   this.coatLength = "short"; 
   this.coatType = "double"; 
} 

function Bulldog() { 
   this.sheddingLevel = 3; 
   this.coatLength = "short"; 
   this.coatType = "smooth"; 
} 

function GoldenRetriever() { 
   this.sheddingLevel = 4; 
   this.coatLength = "medium"; 
   this.coatType = "double"; 
} 

function GermanShepherd() { 
   this.sheddingLevel = 4; 
   this.coatLength = "medium"; 
   this.coatType = "double"; 
} 

function run() { 
   let dogs = []; 
   let factory = new Factory(); 

   dogs.push(factory.createDog("labrador")); 
   dogs.push(factory.createDog("bulldog")); 
   dogs.push(factory.createDog("golden retriever")); 
   dogs.push(factory.createDog("german shepherd")); 

   for (var i = 0, len = dogs.length; i < len; i++) { 
       dogs[i].printInfo(); 
   } 
} 

run();
```

The Factory design pattern controls how objects will be created and provides a quick way to create new objects, as well as a uniform interface that defines the properties your objects will have. You can add as many dog breeds as you want, as long as the methods and properties exposed by the breed types remain the same, they will work perfectly.

However, keep in mind that the Factory pattern can often result in a large number of classes that are difficult to manage.
