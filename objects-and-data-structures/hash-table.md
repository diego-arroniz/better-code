# Hash Table

### Objects (Hash Tables)

In JavaScript, an object is a collection of key-value pairs. This data structure is also called a map, dictionary, or hash-table in other programming languages.

A typical JS object looks like this:

```javascript
const obj = {
  prop1: "I'm",
  prop2: "an",
  prop3: "object"
}
```

We use curly braces to declare the object. Then declare each key followed by a colon, and the corresponding value.

An important thing to mention is that each key has to be unique within the object. You can't have two keys with the same name.

Objects can store both values and functions. When talking about objects, values are called properties, and functions are called methods.

```javascript
const obj = {
  prop1: "Hello!",
  prop3: function() { console.log("I'm a property dude!") }
}
```

To access properties, you can use two different syntaxes, either `object.property` or `object["property"]`. To access methods, we call `object.method()`.

```javascript
console.log(obj.prop1) // "Hello!"
console.log(obj["prop1"]) // "Hello!"
obj.prop3() // "I'm a property dude!"

```

The syntax to assign new values is quite similar:

```javascript
obj.prop4 = 125
obj["prop5"] = "The new prop on the block"
obj.prop6 = () => console.log("yet another example")

console.log(obj.prop4) // 125
console.log(obj["prop5"]) // "The new prop on the block"
obj.prop6() // "yet another example"
```

Like arrays, in JavaScript objects come with many built-in methods that allow us to perform different operations and get information from a given object. A full list can be found here.

Objects are a good way to group together data that have something in common or are somehow related. Also, thanks to the fact that property names are unique, objects come in handy when we have to separate data based on a unique condition.

An example could be counting how many people like different foods:

```javascript
const obj = {
  pizzaLovers: 1000,
  pastaLovers: 750,
  argentinianAsadoLovers: 12312312312313123
}

```
