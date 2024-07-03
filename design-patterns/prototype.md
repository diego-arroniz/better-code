# Prototype

#### Prototype

The Prototype design pattern is a quick and easy way to create new objects from existing objects by cloning them.

First, you create a prototype object, which can be cloned multiple times to create new objects. This is useful when directly instantiating an object is a resource-consuming operation compared to creating a copy of an existing one.

In the following example, you'll see how you can use the Prototype pattern to create new documents based on an established template document:

```javascript
javascriptCopy codefunction Document() { 
   this.header = "Acme Co";
   this.footer = "For internal use only";
   this.pages = 2;
   this.text = "";

   this.addText = function(text) { 
       this.text += text; 
   };

   this.printInfo = function() { 
       console.log("Header: " + this.header + "\nFooter: " + this.footer + "\nPages: " + this.pages + "\nText: " + this.text);
   };
} 

function DocumentPrototype(baseDocument) { 
   this.baseDocument = baseDocument;

   this.clone = function() { 
       let document = new Document();
       document.header = this.baseDocument.header;
       document.footer = this.baseDocument.footer;
       document.pages = this.baseDocument.pages;
       document.text = this.baseDocument.text;
       return document;
   }; 
} 

function run() { 
   let baseDocument = new Document();
   baseDocument.addText("This text was added before cloning and will be common in both documents. ");
   let prototype = new DocumentPrototype(baseDocument);

   let doc1 = prototype.clone();
   let doc2 = prototype.clone();
   doc1.pages = 3;
   doc1.addText("This is document 1");
   doc2.addText("This is document 2");

   doc1.printInfo();
   /* Output:
       Header: Acme Co
       Footer: For internal use only
       Pages: 3
       Text: This text was added before cloning and will be common in both documents. This is document 1
    */

   doc2.printInfo();
   /* Output:
       Header: Acme Co
       Footer: For internal use only
       Pages: 2
       Text: This text was added before cloning and will be common in both documents. This is document 2
    */
}

run();
```

The Prototype method works great for cases where a large part of your objects share the same values, or when creating a new object from scratch is quite costly. However, it seems like overkill in cases where you only need a few instances of the class.
