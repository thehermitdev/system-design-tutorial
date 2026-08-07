# **Low Level Design or LLD**

Low-Level Design (LLD) plays a crucial role in software development, transforming high-level abstract concepts into detailed, actionable components that developers can use to build the system.

- LLD is the blueprint that guides developers on how to implement specific components of a system, such as classes, methods, algorithms, and data structures.
- Whether we are working on a microservice architecture, a web application, or a mobile app, understanding LLD is essential for building scalable, maintainable, and efficient systems.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260414102919491982/design.webp" />

## **Difference Between HLD and LLD**

HLD and LLD are both important in system design, but they focus on different levels of detail. HLD gives a big-picture view of the system, while LLD focuses on the detailed implementation.

1. **High-Level Design (HLD):** Focuses on overall system architecture, including frameworks, databases, component integration, and how the system works at a broader level.
2. **Low-Level Design (LLD):** Focuses on detailed design of components and modules, including interactions, UML diagrams, behavior, and the algorithms and data structures used.

> **Example:** In an e-commerce system, HLD decides components like user service, payment service, and database, while LLD defines how the “Order” class works, what methods it has, and how it interacts with other classes.

## **Concepts Needed to Create a LLD from given HLD**

For HLD to LLD conversion, we generally use [Unified Modelling Language (UML) diagrams](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-introduction/). Adding to these diagrams we use OOP principles and [SOLID principles](https://www.geeksforgeeks.org/system-design/solid-principle-in-programming-understand-with-real-life-examples/) and design patterns while designing.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260414102919609290/roadmap_to_low_level_design_lld_-660.webp" />

### **Step 1. Understanding Object-Oriented Principles**

User requirements are translated into design using OOP concepts, which form the foundation of Low-Level Design (LLD). A strong understanding of OOP principles helps build maintainable, scalable, and well-structured components.

- **Encapsulation**: Bundling data and the methods that operate on that data within one unit.
- **Inheritance**: Mechanism where a new class can inherit the properties and methods of an existing class.
- **Polymorphism**: Ability of different classes to respond to the same method in different ways.
- **Abstraction**: Hiding the complex implementation details while showing only the essential features of an object.

### **Step 2. Analyzing and Designing Components**

LLD requires you to analyze real-world problems and break them down into object-world problems using OOP concepts. This is a critical step where real-world entities are modeled into objects and classes.

We should focus on:

- Identifying classes and objects based on the system requirements.
- Determining relationships (like associations, inheritance, etc.) between different entities.
- Using SOLID principles to ensure your design is clean, maintainable, and scalable.

### **Step 3. Implementing Design Patterns**

Implementation of object-oriented design is supported by design patterns, which provide reusable solutions to common problems. They help build scalable, maintainable, and efficient systems by following proven best practices.

- **Creational Patterns** (e.g., Singleton, Factory): These patterns deal with object creation mechanisms, trying to create objects in a way that is appropriate to the situation.
- **Behavioral Patterns** (e.g., Observer, Strategy): Focus on communication between objects and how they interact with each other.
- **Structural Patterns** (e.g., Adapter, Composite): These patterns are concerned with simplifying the structure of the system and its components.

### **Step 4. Use of UML Diagram in LLD**

Unified Modeling Language (UML) is used to visually model and design systems, helping transition from HLD to LLD. It clearly represents components and their relationships, making system understanding easier for developers.

- **Class Diagrams**: Represent the structure of the system in terms of its classes and the relationships between them.
- **Sequence Diagrams**: Illustrate how objects interact over time, showing the sequence of method calls.
- **Activity Diagrams**: Show the workflow or activities of a system component.
- **State Diagrams**: Represent the different states of a component or object and the transitions between these states.
- **Use Case Diagrams**: Define the functional requirements of the system by showing different user interactions.

These diagrams play a significant role in LLD, providing a clear visual representation of the components and their interactions.

### **5. Implementing SOLID Principles**

These are sets of 5 principles(rules) that are strictly followed as per requirements of the system or requirements for optimal designing. In order to write scalable, flexible, maintainable, and reusable code:

1. Single-responsibility principle (SRP)
2. Open-closed principle (OCP)
3. Liskov’s Substitution Principle(LSP)
4. Interface Segregation Principle (ISP)
5. Dependency Inversion Principle (DIP)

It's important to keep in mind that SOLID principles are just guidelines and not strict rules to be followed. The key is to strike a balance between following these principles and considering the specific needs and constraints of your business requirement.

## **Benefits**

Low-Level Design offers a detailed and structured approach to building software systems, providing multiple benefits:

- **Clear Component Functionality**: LLD provides a detailed plan for how each part of the software will work, making development and debugging easier.
- **Scalability and Flexibility**: It provides a well-structured design, which makes simpler to update or fix parts of the system without affecting the entire software.
- **Improved Communication**: LLD helps team members communicate more effectively because everyone has a clear understanding of how components are working.
- **Cleaner Code**: Following the design principles in LLD leads to more cleaner, organized code, making it less prone to errors.
- **Faster Coding**: A proper LLD speeds up the coding process because developers can follow the detailed plan made earlier.

## **Best Practices for Low-Level Design(LLD)**

Some of the best practices to form a good Low-Level Design are:

- **Modular Design:** Always try to break down the system into small, independent components that contain specific functionalities.
- **Clear Interfaces:** Clearly define the interfaces for each component, which should include methods, inputs, outputs. This helps in maintaining proper communication between components
- **Use Design Patterns:** Include OOPS Principles to promote code reusability, flexibility and maintainability.
- **Adopt SOLID Principles:** Follow Solid Principles which will lead to more robust and maintainable design.
- **Error Handling:** plan in advance for error handling and validation of the system by including validation checks in the design

## **Roadmap to Learn LLD**

To master Low-Level Design, follow this structured learning path:

### **1. Object-Oriented and Design Principles**

- [**Object-Oriented Programming (OOPS) Concepts**](https://www.geeksforgeeks.org/system-design/object-oriented-programingoop-concepts-for-designing-sytems/)
- [**Object-Oriented Analysis and Design**](https://www.geeksforgeeks.org/software-engineering/object-oriented-analysis-and-design/)
- [**SOLID Principles**](https://www.geeksforgeeks.org/system-design/solid-principle-in-programming-understand-with-real-life-examples/)

### **2. Design Patterns**

- [**Creational Design Patterns**](https://www.geeksforgeeks.org/system-design/creational-design-pattern/)
- [**Behavioral Design Patterns**](https://www.geeksforgeeks.org/system-design/behavioral-design-patterns/)
- [**Structural Design Patterns**](https://www.geeksforgeeks.org/system-design/structural-design-patterns/)
- [**When to choose which design pattern?**](https://www.geeksforgeeks.org/system-design/design-patterns-cheat-sheet-when-to-use-which-design-pattern/)

### **3. UML and Modeling in LLD**

- [**Class Diagrams**](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-class-diagrams/)
- [**Sequence Diagrams**](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-sequence-diagrams/)
- [**Activity Diagrams**](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-activity-diagrams/)
- [**State Diagrams**](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-state-diagrams/)
- [**Use Case Diagrams**](https://www.geeksforgeeks.org/system-design/use-case-diagram/)
- [**Object Diagrams**](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-object-diagrams/)

### **4. LLD Best Practices**

- [**Data Structures and Algorithms for System Design**](https://www.geeksforgeeks.org/system-design/data-structures-and-algorithms-for-system-design/)
- [**Essential Security Measures in System Design**](https://www.geeksforgeeks.org/system-design/essential-security-measures-in-system-design/)
- [**Introduction to Modularity and Interfaces**](https://www.geeksforgeeks.org/system-design/inroduction-to-modularity-and-interfaces-in-system-design/)
- [**Difference between LLD and HLD**](https://www.geeksforgeeks.org/system-design/difference-between-high-level-design-and-low-level-design/)
- [**Performance vs Scalability**](https://www.geeksforgeeks.org/system-design/performance-vs-scalability-in-system-design/)
- [**Speed vs. Quality**](https://www.geeksforgeeks.org/system-design/speed-vs-quality-in-system-design/)
- [**Coding Standards Best Practices**](https://www.geeksforgeeks.org/system-design/coding-standards-and-best-practices-for-system-design/)

### **5. LLD Case Studies**

- [**Elevator System Low-Level Design**](https://www.geeksforgeeks.org/system-design/elevator-system-low-level-design-lld/)
- [**Tic-Tac-Toe Low-Level Design**](https://www.geeksforgeeks.org/system-design/low-level-design-of-tic-tac-toe-system-design/)
- [**Amazon Low Level Design**](https://www.geeksforgeeks.org/system-design/amazon-low-level-designlld/)
- [**Vending Machine Low Level Design**](https://www.geeksforgeeks.org/system-design/vending-machine-low-level-design/)

### **6. Interview Preparation**

- [**How to Prepare for Low-Level Design Interviews?**](https://www.geeksforgeeks.org/system-design/how-to-prepare-for-low-level-design-interviews/)
- [**Top Low-Level Design(LLD) Interview Questions 2024**](https://www.geeksforgeeks.org/system-design/top-low-level-system-designlld-interview-questions-2024/)
- [**Best Books for Learning Low-Level Design(LLD) 2024**](https://www.geeksforgeeks.org/system-design/best-books-for-learning-low-level-designlld-2024/)
