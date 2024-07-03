# Prototypes

## Prototypes

JavaScript is a prototype-based language, so understanding the prototype object is one of the most important concepts that JavaScript professionals need to know.

### Prototype Object

For clarity, let's examine the following example:

```javascript
function Point2D(x, y) {
  this.x = x;
  this.y = y;
}
```

When the `Point2D` function is declared, a default property called `prototype` will be created for it (note that in JavaScript, a function is also an object). The `prototype` property is an object that contains a `constructor` property, and its value is the `Point2D` function: `Point2D.prototype.constructor = Point2D`. And when you call `Point2D` with the reserved word `new`, the newly created objects will inherit all properties from `Point2D.prototype`. To verify this, you can add a method called `move` to `Point2D.prototype` as follows:

```javascript
javascriptCopy codePoint2D.prototype.move = function(dx, dy) {
  this.x += dx;
  this.y += dy;
};

var p1 = new Point2D(1, 2);
p1.move(3, 4);
console.log(p1.x); // 4
console.log(p1.y); // 6
```

The `Point2D.prototype` is called the prototype object or the prototype of the `p1` object and any other object created with the `new Point2D(...)` syntax. You can add as many properties to the `Point2D.prototype` object as you want. Typically, methods are declared in `Point2D.prototype`, and other properties are declared in the constructor function.

Built-in objects in JavaScript are constructed similarly. For example:

* The prototype of objects created with the `new Object()` or `{}` syntax is `Object.prototype`.
* The prototype of arrays created with the `new Array()` or `[]` syntax is `Array.prototype`.

And it is the same with other built-in objects like `Date` and `RegExp`.

`Object.prototype` is inherited by all objects and has no prototype (its prototype is `null`).

#### Prototype Chain

The mechanism of the prototype chain is simple: when you access a property `p` on the object `obj`, the JavaScript engine will look for this property within the `obj` object. If the engine fails to find it, it continues to search in the prototype of the `obj` object and so on until it reaches `Object.prototype`. If the search finishes without finding anything, the result will be `undefined`.

#### Classes

In ES2016, we can now use the `class` keyword, as well as the previously mentioned methods to manipulate the `prototype`. JavaScript classes are attractive to developers with experience in object-oriented programming, but they essentially do the same as before.

```javascript
javascriptCopy codeclass Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }

  get area() {
    return this.calcArea();
  }

  calcArea() {
    return this.height * this.width;
  }
}

const square = new Rectangle(10, 10);

console.log(square.area); // 100
```

This is basically the same as:

```javascript
javascriptCopy codefunction Rectangle(height, width) {
  this.height = height;
  this.width = width;
}

Rectangle.prototype.calcArea = function calcArea() {
  return this.height * this.width;
};
```

The `getter` and `setter` methods in classes bind an object property to a function that will be called when that property is looked up. This is just syntactic sugar to help make it easier to look up or set properties.

***

**Source:** [JavaScript Prototypes Explained with Examples](https://www.freecodecamp.org/espanol/news/prototipo-javascript-expliacado-con-ejemplos/)
