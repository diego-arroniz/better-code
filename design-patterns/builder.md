# Builder

#### Builder

The Builder pattern is one of the more complex and flexible creational design patterns in JavaScript. It allows you to build the features of your product one by one, providing you with total control over how your object is built, while abstracting the internal details.

In the intricate example below, you'll see the Builder design pattern in action with a Director to help make pizzas!

```javascript
function PizzaBuilder() { 
   let base; 
   let sauce; 
   let cheese; 
   let toppings = []; 

   function Pizza(base, sauce, cheese, toppings) { 
       this.base = base; 
       this.sauce = sauce; 
       this.cheese = cheese; 
       this.toppings = toppings; 

       this.printInfo = function() { 
           console.log("This pizza has " + this.base + " base with " + this.sauce + " sauce " 
           + (this.cheese !== undefined ? "with cheese. " : "without cheese. ") 
           + (this.toppings.length !== 0 ? "It has the following toppings: " + toppings.toString() : "")); 
       }; 
   } 

   return { 
       addFlatbreadBase: function() { 
           base = "flatbread"; 
           return this; 
       }, 
       addTomatoSauce: function() { 
           sauce = "tomato"; 
           return this; 
       }, 
       addAlfredoSauce: function() { 
           sauce = "alfredo"; 
           return this; 
       }, 
       addCheese: function() { 
           cheese = "parmesan"; 
           return this; 
       }, 
       addOlives: function() { 
           toppings.push("olives"); 
           return this; 
       }, 
       addJalapeno: function() { 
           toppings.push("jalapeno"); 
           return this; 
       }, 
       cook: function() { 
           if (base === null){ 
               console.log("Can't make a pizza without a base"); 
               return; 
           } 
           return new Pizza(base, sauce, cheese, toppings); 
       } 
   }; 
} 

function PizzaShop() { 
   return { 
       makePizzaMargherita: function() { 
           pizzaBuilder = new PizzaBuilder(); 
           pizzaMargherita = pizzaBuilder.addFlatbreadBase().addTomatoSauce().addCheese().addOlives().cook(); 
           return pizzaMargherita; 
       }, 
       makePizzaAlfredo: function() { 
           pizzaBuilder = new PizzaBuilder(); 
           pizzaAlfredo = pizzaBuilder.addFlatbreadBase().addAlfredoSauce().addCheese().addJalapeno().cook(); 
           return pizzaAlfredo; 
       }, 
       makePizzaMarinara: function() { 
           pizzaBuilder = new PizzaBuilder(); 
           pizzaMarinara = pizzaBuilder.addFlatbreadBase().addTomatoSauce().addOlives().cook();
          return pizzaMarinara;
       }
   };
}

function run() {
   let pizzaShop = new PizzaShop();

   let pizzaMargherita = pizzaShop.makePizzaMargherita();
   pizzaMargherita.printInfo();
   // Output: This pizza has flatbread base with tomato sauce with cheese. It has the following toppings: olives

   let pizzaAlfredo = pizzaShop.makePizzaAlfredo();
   pizzaAlfredo.printInfo();
   // Output: This pizza has flatbread base with alfredo sauce with cheese. It has the following toppings: jalapeno

   let pizzaMarinara = pizzaShop.makePizzaMarinara();
   pizzaMarinara.printInfo();
   // Output: This pizza has flatbread base with tomato sauce without cheese. It has the following toppings: olives

   let chef = PizzaBuilder();
   let customPizza = chef.addFlatbreadBase().addTomatoSauce().addCheese().addOlives().addJalapeno().cook();
   customPizza.printInfo();
   // Output: This pizza has flatbread base with tomato sauce with cheese. It has the following toppings: olives,jalapeno
}

run();

```

You can connect the Builder with a Director, like the `PizzaShop` class in the example above, to predefine a set of steps to follow each time you build a standard variant of your product, i.e., a specific recipe for your pizzas.

The only problem with this design pattern is that it is quite complex to set up and maintain. However, adding new features this way is easier than with the Factory method.
