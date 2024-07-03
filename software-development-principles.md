# Software Development Principles

## Development Principles

### SOLID Principles

S.O.L.I.D. is a mnemonic acronym for five design principles intended to make software designs more understandable, flexible, and maintainable.

The principles included in S.O.L.I.D. are:

* **S:** Single Responsibility
* **O:** Open/Closed
* **L:** Liskov Substitution
* **I:** Interface Segregation
* **D:** Dependency Inversion

Applying these principles will greatly facilitate work, both one's own and others' (it is very likely that our code will be read by many other developers throughout its lifecycle). Some advantages of applying them are:

* Facilitating code maintenance.
* Reducing the complexity of adding new functionalities.
* Increasing the reusability of pieces and components.
* Improving the quality and understanding of the code.

#### Single Responsibility Principle (SRP)

The single responsibility principle states that a software module should have one and only one reason to change. This reason to change is what is understood as responsibility.

“Gather together the things that change for the same reasons. Separate those things that change for different reasons.”

This principle is closely related to the concepts of coupling and cohesion. We want to increase the cohesion between things that change for the same reasons and decrease the coupling between things that change for different reasons. This principle is about limiting the impact of a change. Having more than one responsibility also makes the code difficult to read, test, and maintain, i.e., it makes the code less flexible.

Among the advantages of applying this principle, we find that if a change is needed, it will be easy to detect as it will be isolated in a clearly defined and understandable class, minimizing collateral effects on other classes. Some real-life examples are: if the way an item is purchased changes, we will not have to modify the code responsible for storing it. If the database changes, we won't have to fix every piece of code where it is used.

#### Open/Closed Principle (OCP)

This principle tells us that software modules should be open for extension but closed for modification. What does this mean?

* **Open for extension:** This means that the behavior of the module can be extended. As application requirements change, we can extend the module with new behaviors that meet those changes. In other words, we can change what the module does.
* **Closed for modification:** A module will be closed if it has a stable and well-defined description (interface). Extending the behavior of a module should not affect the existing code in the module, i.e., the original code of the module should not have to be modified.

The way to implement this principle in the practical world is through polymorphism, either by interfaces or abstract classes.

#### Liskov Substitution Principle (LSP)

“If it looks like a duck, swims like a duck, but needs batteries, you probably have the wrong abstraction.”

The Liskov substitution principle tells us that objects of a program should be replaceable with instances of their subtypes without altering the correct functioning of the program. Basically, if in some part of our code we are using a class, and this class is extended, we have to be able to use any of the child classes and the program should still be valid. This forces us to ensure that when we extend a class, we are not altering the behavior of the parent class. This principle helps us use inheritance correctly and shows us that we should not automatically map the real world into an object-oriented model, as there is no one-to-one equivalence between both models.

#### Interface Segregation Principle (ISP)

The interface segregation principle states that many client-specific interfaces are better than one general-purpose interface. When clients are forced to use interfaces they do not fully utilize, they are subject to changes in that interface. This ultimately results in unnecessary coupling between clients. In other words, when a client depends on a class that implements an interface whose functionality this client does not use but other clients do, this client will be affected by changes that other clients force on the class in question. We should try to avoid this type of coupling whenever possible. This is achieved by separating interfaces into smaller, more specific ones.

#### Dependency Inversion Principle (DIP)

The dependency inversion principle tells us that software entities should depend on abstractions, not implementations. Furthermore, high-level modules should not depend on low-level modules. Both should depend on abstractions.

By applying this principle, we hide implementation details, gaining flexibility. When we are testing, we can replace real dependencies with mocked objects. Thanks to this flexibility, we can replace components without affecting the clients that consume them, as they depend on the abstraction and not on the concrete implementation. The aim is for there to be no direct dependencies between modules but for them to depend on abstractions. This way, our modules can be more easily reusable. It is essential that the abstraction is defined based on the needs of the module or client and not on the capabilities of the implementation; otherwise, the abstraction would be quite coupled to the implementation, thus having less flexibility.

***

**Source:** [Software Design Principles and Patterns - Autentia](https://www.autentia.com/wp-content/uploads/libros/SoftwareDesign\_PrincipiosyPatrones-Autentia.pdf)
