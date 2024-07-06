# Software Architecture

## Application Architecture

Application architecture describes the patterns and techniques used to design and develop applications. It provides a blueprint and best practices to follow when designing a well-structured application.

### Types of Application Architecture

When deciding which application architecture to use for a new application, or when evaluating the one currently in use, start by determining your strategic goals. This will allow you to design an architecture that supports your goals, rather than first choosing one and then trying to fit applications into it.

Consider how frequently you want to release updates to meet operational or customer needs, as well as the features required for business objectives or development needs. The ability to quickly deliver new services and features to customers is one of the key competitive advantages a company can offer, making a difference. If companies streamline development, they can release new features more frequently and implement updates as soon as they discover a vulnerability.

Currently, the main application architectures, based on service relationships, are monolithic architecture and N-tier (directly connected), microservices (decoupled), and event-driven and service-oriented architectures (low coupling).

#### Layered Architecture or N-tier

It is a type of traditional architecture commonly used for designing on-premises and enterprise applications, often associated with legacy applications. In this architecture, there are several layers or levels (often three, but there may be more) composing the application, each serving a particular function. Layers help manage dependencies and execute logical functions. In a layered architecture, these are organized horizontally, so they can only utilize functions from the lower layers. This means that a layer can only access resources from the one immediately below it or any of the lower layers.

<figure><img src=".gitbook/assets/image (18).png" alt="" width="264"><figcaption></figcaption></figure>

#### Monolithic Architecture

Monoliths are another type of architecture associated with legacy systems; they are single-application stacks containing all functions within each application. They are directly connected, both in service interaction and in how they are developed and deployed.

This means that updating or adjusting a single aspect of a monolithic application not only impacts the application itself but also the underlying infrastructure. A single change in the application's code implies a complete re-launch. Hence, updates and new versions typically occur once or twice a year and should not include new features, but only general maintenance. In contrast, modern architectures strive to release services by function or business capability to provide more agility.

<figure><img src=".gitbook/assets/image (19).png" alt="" width="317"><figcaption></figcaption></figure>

#### Microservices Architecture

Microservices are not just a type of architecture but also a way of approaching software development. With microservices, applications are divided into their smallest elements, which are independent of each other. Each of these elements or processes is a microservice. Microservices are distributed and have a low level of coupling to avoid influencing others. This architecture brings benefits in terms of dynamic scalability and fault tolerance: individual services can be scaled up as needed without requiring heavy infrastructure, or they can perform failover without affecting other services. The goal of using a microservices architecture is to deliver quality software more quickly. You can develop multiple microservices simultaneously without needing to redesign or implement the entire application after making changes, as services are deployed independently. Thanks to this, multiple developers can work on their individual services simultaneously, rather than updating the entire application, reducing development time and enabling more frequent release of new features. Together with DevOps teams and APIs, microservices in containers form the foundation of cloud-native applications.

<figure><img src=".gitbook/assets/image (20).png" alt="" width="339"><figcaption></figcaption></figure>

#### Event-Driven Architecture

In a system like this, capturing, communicating, processing, and persisting events form the central structure of the solution. This differs from the traditional request-based model. Events are significant occurrences or changes in the state of hardware or software within a system. Events happen due to internal or external stimuli. Event-driven architecture allows for minimal coupling, making it a good choice for distributed and modern application architectures. This architecture consists of event consumers and producers. The producer detects events and represents them as messages. It does not know the event's consumer or the result it will generate. After an event is detected, it is transmitted from the producer to consumers through event channels, where they are processed asynchronously with an event processing platform. Such an architecture can be based on a publish/subscribe model or an event stream model. The publish/subscribe model relies on subscriptions to an event stream. Once an event is generated or published, it is sent to subscribers who need to be informed about it. This differs from the event stream model, where consumers do not subscribe to an event stream but can read it from any part and join it at any time. Events are captured as they occur from sources like networks, applications, and Internet of Things (IoT) devices. This enables event producers and consumers to share information about state and response in real-time.

<figure><img src=".gitbook/assets/image (21).png" alt="" width="362"><figcaption></figcaption></figure>

#### Service-Oriented Architecture

Service-Oriented Architecture (SOA) is a well-established software design style resembling microservices architecture. SOA structures applications into independent and reusable services that communicate through an Enterprise Service Bus (ESB). In this architecture, individual services are organized around a specific business process and adhere to a communication protocol (such as SOAP, ActiveMQ, or Apache Thrift). Additionally, they can be accessed through an ESB platform. A frontend application utilizes this set of services, integrated through an ESB, to deliver value to a business or customer.

<figure><img src=".gitbook/assets/image (23).png" alt="" width="331"><figcaption></figcaption></figure>

***

Source: ¿Qué es una arquitectura de aplicaciones? Tipos de arquitecturas de aplicaciones (redhat.com) [https://www.redhat.com/es/topics/cloud-native-apps/what-is-an-application-architecture](https://www.redhat.com/es/topics/cloud-native-apps/what-is-an-application-architecture)
