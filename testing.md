# Testing

## Testing

Testing is the process of executing a program to find errors. To make our software perform well it should be error-free.

### Principles of Testing

1. All the tests should meet the customer’s requirements.
2. To make our software testing should be performed by a third party.
3. Exhaustive testing is not possible. As we need the optimal amount of testing based on the risk assessment of the application.
4. All the tests to be conducted should be planned before implementing it.
5. It follows the Pareto rule (80/20 rule) which states that 80% of errors come from 20% of program components.
6. Start testing with small parts and extend it to large parts.

### Advantages of Software Testing

1. Improved software quality and reliability.
2. Early identification and fixing of defects.
3. Improved customer satisfaction.
4. Increased stakeholder confidence.
5. Reduced maintenance costs.

### Disadvantages of Software Testing

1. Time-Consuming and adds to the project cost.
2. This can slow down the development process.
3. Not all defects can be found.
4. Can be difficult to fully test complex systems.
5. Potential for human error during the testing process.

### Types of Testing

1. Unit Testing
2. Integration Testing
3. System Testing
4. Functional Testing
5. Acceptance Testing
6. Smoke Testing
7. Regression Testing
8. Performance Testing
9. Security Testing
10. User Acceptance Testing

#### Unit Testing

Unit testing is a method of testing individual units or components of a software application. It is typically done by developers and is used to ensure that the individual units of the software are working as intended. Unit tests are usually automated and are designed to test specific parts of the code, such as a particular function or method. Unit testing is done at the lowest level of the software development process, where individual units of code are tested in isolation.

**Advantages of Unit Testing:**

1. It helps to identify bugs early in the development process before they become more difficult and expensive to fix.
2. It helps to ensure that changes to the code do not introduce new bugs.
3. It makes the code more modular and easier to understand and maintain.
4. It helps to improve the overall quality and reliability of the software.

#### Integration Testing

Integration testing is a method of testing how different units or components of a software application interact with each other. It is used to identify and resolve any issues that may arise when different units of the software are combined. Integration testing is typically done after unit testing and before functional testing and is used to verify that the different units of the software work together as intended.

**Different Ways of Performing Integration Testing:**

* Top-down integration testing: It starts with the highest-level modules and differentiates them from lower-level modules.
* Bottom-up integration testing: It starts with the lowest-level modules and integrates them with higher-level modules.
* Big-Bang integration testing: It combines all the modules and integrates them all at once.
* Incremental integration testing: It integrates the modules in small groups, testing each group as it is added.

**Advantages of Integration Testing:**

1. It helps to identify and resolve issues that may arise when different units of the software are combined.
2. It helps to ensure that the different units of the software work together as intended.
3. It helps to improve the overall reliability and stability of the software.
4. Integration testing is essential for complex systems where different components are integrated together.
5. As with unit testing, integration testing should be used in combination with other types of testing such as unit testing, functional testing, and acceptance testing to ensure that the software meets the needs of its users.

#### Regression Testing

Regression testing is a testing method used to ensure that changes made to the software do not introduce new bugs or cause existing functionality to break. It is typically done after changes have been made to the code, such as bug fixes or new features, and is used to verify that the software still works as intended.

**Regression testing can be performed in different ways:**

* Retesting: This involves testing the entire application or specific functionality that was affected by the changes.
* Re-execution: This involves running a previously executed test suite to ensure that the changes did not break any existing functionality.
* Comparison: This involves comparing the current version of the software with a previous version to ensure that the changes did not break any existing functionality.

**Advantages of Regression Testing:**

1. It helps to ensure that changes made to the software do not introduce new bugs or cause existing functionality to break.
2. It helps to ensure that the software continues to work as intended after changes have been made.
3. It helps to improve the overall reliability and stability of the software.
4. Regression testing is an ongoing process that should be done throughout the software development lifecycle to ensure that the software continues to work as intended. It should be automated as much as possible to save time and resources.

#### Smoke Testing

Smoke Testing is done to make sure that the software under testing is ready or stable for further testing. It is called a smoke test as the testing of an initial pass is done to check if it did not catch fire or smoke in the initial switch-on.

**Example:**

If the project has 2 modules, before going to the module make sure that module 1 works properly.

#### Alpha Testing

Alpha testing is a type of validation testing. It is a type of acceptance testing that is done before the product is released to customers. It is typically done by QA people.

**Example:**

When software testing is performed internally within the organization.

#### Beta Testing

The beta test is conducted at one or more customer sites by the end-user of the software. This version is released for a limited number of users for testing in a real-time environment.

**Example:**

When software testing is performed for a limited number of people.

#### System Testing

System Testing is carried out on the whole system in the context of either system requirement specifications or functional requirement specifications or in the context of both. The software is tested such that it works fine for the different operating systems. It is covered under the black box testing technique. In this, we just focus on the required input and output without focusing on internal work. In this, we have security testing, recovery testing, stress testing, and performance testing.

#### Stress Testing

In Stress Testing, we give unfavorable conditions to the system and check how they perform in those conditions.

#### Acceptance Testing

Acceptance testing is done by the customers to check whether the delivered products perform the desired tasks or not, as stated in the requirements.

***

**Source:** Types of Software Testing - GeeksforGeeks

[https://www.geeksforgeeks.org/types-software-testing/](https://www.geeksforgeeks.org/types-software-testing/)
