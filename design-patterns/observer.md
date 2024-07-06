# Observer

#### Observer

The Observer pattern provides an alternative solution to the problem of multi-object interaction.

Instead of allowing each object to communicate with each other through a designated mediator, the Observer pattern allows them to observe each other. Objects are designed to emit events when they try to send data or control, and other objects that are "listening" to these events can then receive them and interact based on their content.

Here is a simple demonstration of how to send newsletters to multiple people through the Observer pattern:

```javascript
function Newsletter() {
    this.subscribers = [];

    this.subscribe = function(subscriber) {
        this.subscribers.push(subscriber);
    };

    this.unsubscribe = function(subscriber) {
        this.subscribers = this.subscribers.filter(function (element) {
            if (element !== subscriber) return element;
        });
    };

    this.publish = function(post) {
        this.subscribers.forEach(function(element) {
            element.receiveNewsletter(post);
        });
    };
}

function Reader(name) {
    this.name = name;

    this.receiveNewsletter = function(post) {
        console.log("Newsletter received by " + name + "!: " + post);
    };
}

function run() {
    let rick = new Reader("Rick");
    let morty = new Reader("Morty");

    let newsletter = new Newsletter();

    newsletter.subscribe(rick);
    newsletter.publish("This is the first of the many posts in this newsletter");
    // Output:
    // Newsletter received by Rick!: This is the first of the many posts in this newsletter

    newsletter.subscribe(morty);
    newsletter.publish("This is the second of the many posts in this newsletter");
    // Output:
    // Newsletter received by Rick!: This is the second of the many posts in this newsletter
    // Newsletter received by Morty!: This is the second of the many posts in this newsletter

    newsletter.unsubscribe(rick);
    newsletter.publish("This is the third of the many posts in this newsletter");
    // Output:
    // Newsletter received by Morty!: This is the third of the many posts in this newsletter
}

run();
```

While the Observer pattern is a clever way to pass control and data, it is more suitable for situations where there are a large number of emitters and receivers interacting with each other through a limited number of connections. If all objects establish one-to-one connections, you lose the advantage gained by publishing and subscribing to events, as there will always be a single subscriber for each publisher (when it would have been better managed via a direct line of communication between them).

Additionally, the Observer design pattern can cause performance issues if subscription events are not properly managed. If an object continues to subscribe to another object even when it no longer needs it, it will not be eligible for garbage collection and will increase the application's memory consumption.
