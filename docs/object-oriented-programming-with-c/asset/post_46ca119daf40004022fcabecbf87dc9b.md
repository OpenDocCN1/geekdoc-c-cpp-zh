
![](img/62b7c32e48e4f960a8dc2825a7119fb2_692_0.png)

**Fig. 17.7** *Instances of objects*

![](img/62b7c32e48e4f960a8dc2825a7119fb2_692_1.png)

**Fig. 17.8** *Message communication between objects*

![](img/62b7c32e48e4f960a8dc2825a7119fb2_693_0.png)

Base class

Derived class

**Fig. 17.9** *Inheritance relationship*

![](img/62b7c32e48e4f960a8dc2825a7119fb2_694_0.png)

![](img/62b7c32e48e4f960a8dc2825a7119fb2_695_0.png)

![](img/62b7c32e48e4f960a8dc2825a7119fb2_696_0.png)

**Fig. 17.12** *Hierarchical chart*

![](img/62b7c32e48e4f960a8dc2825a7119fb2_696_1.png)

**Fig. 17.13** *Client-server relationship*

5. Establishing inter-connections (collaborations) between the objects in terms of services required and services rendered.

Although we have shown the above tasks as a series of discrete steps, the last three activities are carried out inter-dependently as shown in Fig. 17.15

![](img/62b7c32e48e4f960a8dc2825a7119fb2_698_0.png)

**Fig. 17.15** *Activities of object-oriented analysis*

## Problem Understanding

The first step in the analysis process is to understand the problem of the user. The problem statement should be refined and redefined in terms of computer system engineering that could suggest a computer-based solution. The problem statement should be stated, as far as possible, in a single, grammatically correct sentence. This will enable the software engineers to have a highly focussed attention on the solution of the problem. The problem statement provides the basis for drawing the requirements specification of both the user and the software.

## Requirements Specification

Once the problem is clearly defined, the next step is to understand what the proposed system is required to do. It is important at this stage to generate a list of user requirements. A clear understanding should exist between the user and the developer of what is required. Based on the user requirements, the specifications for the software should be drawn. The developer should state clearly

- What outputs are required.
- What processes are involved to produce these outputs.
- What inputs are necessary.
- What resources are required.

These specifications often serve as a reference to test the final product for its performance of the intended tasks.

## Identification of Objects

Objects can often be identified in terms of the real-world objects as well as the abstract objects. Therefore, the best place to look for objects is the application itself. The application may be analyzed by using one of the following two approaches:

- 1. Data flow diagrams (DFD)
- 2. Textual analysis (TA)

### Data Flow Diagram

The application can be represented in the form of a data flow diagram indicating how the data moves from one point to another in the system. The boxes and data stores in the data flow diagram are good candidates for the objects. The process bubbles correspond to the procedures. Figure 17.16 illustrates a typical data flow diagram. It is also known as a data flow graph or a bubble chart.

A DFD can be used to represent a system at any level of abstraction. For example, the DFD shown in Fig. 17.16 may be

![](img/62b7c32e48e4f960a8dc2825a7119fb2_701_0.png)

**Fig. 17.17** *Fundamental data flow diagram*

**Table 17.3 — Types of nouns**

| Type of noun | Meaning | Example |
|---|---|---|
| Common noun | Describe classes of things (entities) | Vehicle, customer income, deduction |
| Proper noun | Names of specific things | Maruti car, John, ABC company |
| Mass or abstract noun | Describe a quality, Quantity or an activity associated with a noun | Salary-income house-loan, feet, traffic |

It is important to note that the context and semantics must be used to determine the noun categories. A particular word may mean a common noun in one context and a mass or abstract noun in another.

These approaches are only a guide and not the ultimate tools. Creative perception and intuition of the experienced developers play an important role in identifying the objects.

Using one of the above approaches, prepare a list of objects for the application problem. This might include the following tasks:

- 1. Prepare an object table.
- 2. Identify the objects that belong to the solution space and those which belong to the problem space only. The problem space objects are outside the software boundary.
- 3. Identify the attributes of the solution space objects.

Remember that not all the nouns will be of interest to the final realization of the solution. Consider the following requirement statements of a system:

## Identification of Services

Once the objects in the solution space have been identified, the next step is to identify a set of services that each object should offer. Services are identified by examining all the verbs and verb phrases in the problem description statement. Verbs which can note actions or occurrences may be classified as shown in [Table 17.4].

**Table 17.4 — Classification of verbs**

| Types of verb | Meaning | Examples |
|---|---|---|
| Doing verbs | operations | read, get, display, buy |
| Being verbs | classifications | is an, belongs to |
| Having verbs | composition | has an, is part of |
| Compare verbs | operations | is less than, is equal to |
| Stative verbs | invariance-condition | to be present, are owned |

*Doing verbs* and *compare verbs* usually give rise to services (which we call as functions in C++). *Being verbs* indicate the existence of the classification structure while *having verbs* give rise to the composition structures.

## Establishing Interconnections

This step identifies the services that objects provide and receive. We may use an information flow diagram (IFD) or an entity-relationship (ER) diagram to enlist this information. Here, we must establish a correspondence between the services and the actual information (messages) that are being communicated.

## 17.7 Steps in Object-Oriented Design

Design is concerned with the mapping of objects in the problem space into objects in the solution space, and creating an overall structure (architectural model) and computational models of the system. This stage normally uses the bottom-up approach to build the

(functions) are improved to denote clearly the kind of processing involved.

### Class Dependencies

Analysis of relationships between the classes is central to the structure of a system. Therefore, it is important to identify appropriate classes to represent the objects in the solution space and establish their relationships. The major relationships that are important in the context of design are:

- 1. Inheritance relationships.
- 2. Containment relationships.
- 3. Use relationships.

**Inheritance relationship** is the highest relationship that can be represented in C++. It is a powerful way of representing a hierarchical relationship directly. The real appeal and power of the inheritance mechanism is that it allows us to reuse a class that is almost, but not exactly, what we want and to tailor the class in a way that it does not introduce any unwanted side effects into the rest of the class. We must review the attributes and operations of the classes and prepare an *inheritance relationship* table as shown in [Table 17.5].

**Table 17.5  _Inheritance relationship table_**

| Class | Depends on |
|---|---|
| A | ...... |
| B | A |
| C | A |
| D | B |
| B1 | B |
| B2 | B |

**Containment relationship** means the use of an object of a class as a member of another class. This is an alternative and complementary technique to use the class inheritance. But, it is often a tricky issue to choose between the two techniques. Normally, if there is a need to override attributes or functions, then the inheritance is the best choice. On the other hand, if we want to represent a property by a variety of types, then the containment relationship is the right method to follow. Another place where we need to use an object as a member is when we need to pass an attribute of a class as an argument to the constructor of another class. The “another” class must have a member object that represents the argument. The inheritance represents _is_a_ relationship and the containment represents _has_a_ relationship.

**Use relationship** gives information such as the various classes a class uses and the way it uses them. For example, a class **A** can use classes **B** and **C** in several ways:

- **A** reads a member of **B**.
- **A** calls a member of **C**.
- **A** creates **B** using new operator.

The knowledge of such relationships is important to the design of a program.

### Organization of Class Hierarchies

In the previous step, we examined the inheritance relationships. We must re-examine them and create a class hierarchy so that we can reuse as much data and/or functions that have been designed already. Organization of the class hierarchies involves identification of common attributes and functions among a group of related classes and then combining them to form a new class. The new class will serve as the super class and the others as subordinate classes (which derive attributes from the super class). The new class may or may not have the meaning of an object by itself. If the object is created purely to combine the common attributes, it is called an _abstract class_.
