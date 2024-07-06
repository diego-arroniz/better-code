# Composite

#### Composite

The Composite design pattern helps you structure and manage similar objects and entities easily. The basic idea of the Composite pattern is that objects and their logical containers can be represented using a single abstract class (which can store data/methods related to the object and references to itself for the container).

It makes more sense to use the Composite pattern when your data model resembles a tree structure. However, you should not try to convert a non-tree data model into a tree data model just to use the Composite pattern, as doing so can often reduce flexibility.

In the following example, you'll see how you can use the Composite design pattern to build a packaging system for e-commerce products that can also calculate the total order value per package:

```javascript
function Product(name, price) { 
   this.name = name; 
   this.price = price;

   this.getTotalPrice = function() { 
       return this.price; 
   };
}

function Box(name) { 
   this.contents = []; 
   this.name = name;

   this.add = function(content) { 
       this.contents.push(content); 
   };

   this.remove = function(content) { 
       const index = this.contents.indexOf(content);
       if (index !== -1) { 
           this.contents.splice(index, 1); 
       }
   };

   this.getContent = function(position) { 
       return this.contents[position]; 
   };

   this.getTotalCount = function() { 
       return this.contents.length; 
   };

   this.getTotalPrice = function() { 
       let totalPrice = 0; 
       for (let i = 0; i < this.getTotalCount(); i++) { 
           totalPrice += this.getContent(i).getTotalPrice(); 
       } 
       return totalPrice; 
   };
}

function run() { 
   const mobilePhone = new Product("mobile phone", 1000);
   const phoneCase = new Product("phone case", 30);
   const screenProtector = new Product("screen protector", 20);

   const pen = new Product("pen", 2);
   const pencil = new Product("pencil", 0.5);
   const eraser = new Product("eraser", 0.5);
   const stickyNotes = new Product("sticky notes", 10);

   const electronicsBox = new Box("electronics");
   electronicsBox.add(mobilePhone);
   electronicsBox.add(phoneCase);
   electronicsBox.add(screenProtector);

   const stationeryBox = new Box("stationery");
   stationeryBox.add(pen);
   stationeryBox.add(pencil);
   stationeryBox.add(eraser);
   stationeryBox.add(stickyNotes);
     
   const package = new Box("package");
   package.add(electronicsBox);
   package.add(stationeryBox);

   console.log("Total order price: USD " + package.getTotalPrice());
   // Output: USD 1063
}

run();

  
```

The biggest drawback of using the Composite pattern is that changes to the component interfaces can be very complicated in the future. Designing the interfaces requires time and effort, and the tree-like nature of the data model can make it very difficult to introduce changes at will.
