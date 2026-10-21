
In object-oriented systems, each object belongs to a class. An object that belongs to a certain class is called an instance of the class. We therefore often use objects and instance as synonyms.

An instance is an object created from a class. The class describes the (behavior and information) structure of the instance, while the current state of the instance is defined by the operations performed on the instance.

## 1.4 POLYMORPHISM

Instances, created from classes, will together provide us with the dynamic behavior that we wish to model. It is when these instances start to communicate with each other that the system’s behavior is performed. An instance may know of other instances to which stimuli can be sent. If an instance sends a stimulus to another instance, but does not have to be aware of which class the receiving instance belongs to, we say that we have polymorphism. Polymorphism means, at least in object-oriented contexts, that the sending instance does not need to know the receiving instance’s class and that this class can be any class. Polymorphism means that the sender of a stimulus.

- Does not need to know the receiving instance’s class.
- The receiving instance can belong to an arbitrary class.

## 1.5 INHERITANCE

If class B inherits class A, then both the operations and the information structure described in class A will become part of class B.

By means of inheritance, we can show similarities between classes and describe these similarities in a class, which other classes can inherit. Hence, we can reuse common descriptions. Inheritance is therefore often promoted as a core idea for reuse in the software industry. However, although inheritance, properly used, is a very useful mechanism in many contexts including reuse, it is not a prerequisite for reuse.

## 1.6 OBJECT-ORIENTED ANALYSIS

The purpose of object-oriented analysis, as with all other analysis, is to obtain an understanding of the application: an understanding depending only on the system’s functional requirements.

Object-oriented analysis contains, in some order, the following activities:

- Finding the object.
- Organizing the objects.
- Describing how the objects interact.
- Defining the operations of the objects.
- Defining the objects internally.

## 1.7 FINDING THE OBJECTS

The objects can be found as naturally occurring entities in the application domain. The aim is to find the essential objects, which are to remain essential throughout the system life cycle. Stability also depends on the fact that modifications often begin from some of these items and therefore are local. For example, in an application for controlling water tank, typically objects would include contained water, regulator, valve and tank.

## 1.8 CONCEPTUAL MODELING

It has been used in several different contexts since it appeared in the 1970s; example analysis of information management system and organization theory. The aim is to create models of the system or organization to be analyzed. The concepts of conceptual modeling is often used as a synonym for data modeling and is often discussed with structuring and the use of the databases.

## 1.9 REQUIREMENTS MODEL

The first transformation made is from the requirement specification to the requirement model. The requirements model consists of:

- (a) A use case model.
- (b) Interface descriptions.
- (c) A problem domain model.

The use case model uses actors and use cases. These concepts are simply an aid to define what exists outside the system (actors) and what should be performed by the system (use case).

## 1.10 ANALYSIS MODEL

We have seen that the requirements model aims to define the limitations of the system and to specify its behavior. When the requirement model has been developed and approved by the system users or orders, we can start to develop the actual system.

This starts with development of the analysis model. Its model aims to structure the system independently of the actual implementation environment. This means that we focus on the logical structure of the system. It is here that we define the stable, robust and maintainable structure that is also extensible.

## 1.11 THE DESIGN MODEL

In the construction process, we construct the system using both the analysis model and the requirements model. First, we create a design model that is a refinement and formalization of the analysis model.

**Design** emphasizes a *conceptual solution* that fulfils the requirements, rather than its implementation. For example, a description of a database schema and software objects. Ultimately, designs can be implemented. As with analysis, the term is best qualified, as in *object design* or *database design*. Analysis and design have been summarized in the phase *do the right thing (analysis), and do the things right (design)*.

## 1.12 THE IMPLEMENTATION MODEL

The implementation model consists of the annotated source code. The information space is the one that the programming language uses. Note that we do not require an Object-oriented Programming language; the technique may be used with any programming language to obtain an object-oriented structure of the system. However, an Object-oriented Programming language is desirable since all fundamental concepts can easily be mapped onto language constructs.

## 1.13 TEST MODEL

The test model is the last model developed in the system development. It describes, simply stated, the result of the testing. The fundamental concepts in testing are mainly the test specification and the test result.

### 1.13.1 Analysis

**Analysis** emphasizes an *investigation* of the problem and requirements, rather than a solution. For example, if a new computerized library information system is desired, how will it be used?

“Analysis” is a broad term, best qualified, as in *requirements analysis* (an investigation of the requirements) or *object analysis* (an investigation of the domain objects).

### 1.13.2 What is Done in Analysis?

Two different models are developed in analysis, the requirement model and the analysis model. The real base is the requirement specification and discussions with the prospective users. For example, the system controls a recycling machine for returnable bottles, cans and crates (used in Europe to hold several bottles).

### 1.13.3 Why Do We have a Construction Process?

We built our system in the construction phase, based on the analysis model and the requirement’s model created during analysis. The construction process lasts until the coding is completed and the code units have been tested. Construction consists of design and implementation.

## 1.14 OBJECT-ORIENTED ANALYSIS AND DESIGN

Object-oriented technology is built upon a sound engineering foundation, whose elements we collectively call the object model. The object model encompasses the principles of abstraction, encapsulation, modularity, hierarchy, typing, concurrency, and persistence. What is important about the object model is that these elements are brought together in a synergistic way?

Let there be no doubt that object-oriented analysis and design is fundamentally different than traditional structured design approaches. It requires a different way of thinking about decomposition and it produces software architectures that are largely outside the realm of the structured design culture. These differences arise from the fact that structures design methods build upon structure programming whereas object-oriented design builds upon object-oriented programming. Object-oriented programming means different things to different people.

## 1.15 THE EVOLUTION OF OBJECT MODEL

The generation of programming languages as we look back upon the relatively briefly yet colorful history of software engineering. We cannot help but notice two sweeping trends. The shift in focus from programming in the small to programming in the large. The evolution of high order programming languages.

### 1.15.1 Foundations of Object Model

Structured design methods evolved to guide developers who were trying to build complex systems using algorithms as their fundamental building blocks. Similarly object-oriented design methods have evolved to help developers exploit the expressive power of object based and object-oriented programming languages using the class and object as basic building blocks.

Object-oriented analysis and design thus represents an evolutionary development, not a revolutionary one; it does not break with advances from the past, but builds upon proven ones. Unfortunately, most programmers today are formally and informally trained only in the principles of structured design.

## 1.16 OBJECT-ORIENTED PROGRAMMING

Object-oriented programming is a method of implementation in which programs are organized as cooperative collections of objects, each of which represents an instance of some class, and whose classes are all members of a hierarchy of classes united via inheritance relationships.

Object-oriented programming uses objects, not algorithms, as its fundamental logical building blocks. Each object is an instance of some class. Classes are related to one another via inheritance relationships. A program may appear to be object-oriented, but if any of these elements is missing, it is not an object-oriented program.

It supports objects that are data abstractions with an interface of named operations and a hidden local state.

- (a) Objects have an associated type (class).
- (b) Types (classes) may inherit attributes from super types (super classes).

## 1.17 OBJECT-ORIENTED DESIGN

Object-oriented design is a method of design encompassing the process of object-oriented decomposition and a notation for depicting both logical and physical as well as static and dynamic models of the system under design.
