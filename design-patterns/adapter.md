# Adapter

#### Adapter

A common problem when creating applications is allowing collaboration between incompatible classes.

A good example to understand this is maintaining backward compatibility. If you write a new version of a class, you'll naturally want it to be easily usable in all places where the old version worked. However, if you make breaking changes, such as removing or updating methods that were crucial for the old version's operation, you may end up with a class that needs all its clients updated to run.

In these cases, the Adapter design pattern can be helpful.

The Adapter design pattern provides an abstraction that bridges the methods and properties of the new class and the old class's methods and properties. It has the same interface as the old class but contains logic to map the old methods to the new ones to perform similar operations. This is similar to how an electrical outlet adapter works between a US-style plug and a European-style plug.

Here's an example:

```javascript
function Robot() { 
   this.walk = function(numberOfSteps) { 
       console.log("walked " + numberOfSteps + " steps"); 
   };

   this.sit = function() { 
       console.log("sit"); 
   };
}

function AdvancedRobot(botName) { 
   this.name = botName;

   this.sit = function() { 
       console.log("sit"); 
   };

   this.rightStepForward = function() { 
       console.log("right step forward"); 
   };

   this.leftStepForward = function() { 
       console.log("left step forward"); 
   };
}

function RobotAdapter(botName) { 
   const robot = new AdvancedRobot(botName);

   this.walk = function(numberOfSteps) { 
       for (let i = 0; i < numberOfSteps; i++) { 
           if (i % 2 === 0) { 
               robot.rightStepForward(); 
           } else { 
               robot.leftStepForward(); 
           } 
       } 
   };

   this.sit = robot.sit;
}

function run() { 
   let robot = new Robot();
   robot.sit(); 
   // Output: sit 
   robot.walk(5); 
   // Output: walked 5 steps 

   robot = new RobotAdapter("my bot");
   robot.sit(); 
   // Output: sit 
   robot.walk(5); 
   // Output: 
   // right step forward 
   // left step forward 
   // right step forward 
   // left step forward 
   // right step forward 
}

run();
```

The main problem with this design pattern is that it adds complexity to your source code. You already had to maintain two different classes, and now you have another class — the Adapter — to maintain.
