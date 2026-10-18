
individual units and the whole system. It requires a detailed plan as to what, when and how to test.

*Maintenance:* After the software has been installed, it may undergo some changes. This may occur due to a change in the user’s requirement, a change in the operating environment, or an error in the software that has not been fixed during the testing. Maintenance ensures that these changes are incorporated wherever necessary.

Each phase of the life cycle has its own goals and outputs. The output of one phase acts as an input to the next phase. Table 17.1 shows typical outputs that could be generated for each phase of the life cycle.

| Phase | Output |
|---|---|
| Problem definition (why) | • Problem statement sheet<br>• Project request |
| Analysis (what) | • Requirements document<br>• Feasibility report<br>• Specifications document<br>• Acceptance test criteria |
| Design (how) | • Design document<br>• Test class design |
| Coding (how) | • Code document (program)<br>• Test plan<br>• User manual |
| Testing (what and how) | • Tested code<br>• Test results<br>• System manual |
| Maintenance | • Maintenance log sheets |

and design and therefore they are known as the structured tools. The recent tools are the third generation ones evolved since late 1980s to suit the *object-oriented* analysis and design.

Table 17.2 shows some of the popular tools used for various development processes under the three categories. Although this categorization is questionable, it gives a fair idea of the growth of the tools during the last three decades.

**Table 17.2** *System development tools*

| Process | First generation | Second generation | Third generation |
|---|---|---|---|
| Physical processes | System flowcharts | Context diagrams | Inheritance graphs<br>Object-relationship charts |
| Data representation | Layout forms<br>Grid charts | Data dictionary | Objects/object dictionary |
| Logical processes | Playscript English narrative | Decision tables & trees<br>Data flow diagrams | Inheritance graphs<br>Data flow diagrams |
| Program representation | Program flowcharts<br>I/O layouts | Structure charts<br>Warnier/Orr diagrams | State change diagrams<br>Ptech diagrams<br>Coad/Yourdon charts |

This section gives an overview of some of the most frequently used first and second generation tools. Object-oriented development tools will be discussed later in this chapter (as and when they are required).

*System flowcharts:* A graphical representation of the important inputs, outputs, and data flow among the key points in the system.

*Program flowcharts:* A graphical representation of the program logic.

*Playscripts:* A narrative description of executing a procedure.

*Layout forms:* A format designed for putting the input data or displaying results.

*Grid charts:* A chart showing the relationship between different modules of a system.

*Context diagrams:* A diagram showing the inputs and their sources and the outputs and their destinations. A context diagram basically outlines the system boundary.

*Data flow diagrams:* They describe the flow of data between the various components of a system. It is a network representation of the system which includes processes and data files.

*Data dictionary:* A structured repository of data about data. It contains a list of terms and their definitions for all the data items and data stores.

*Structure chart:* A graphical representation of the control logic of functions (modules) representing a system.

*Decision table:* A table of contingencies for defining a problem and the actions to be taken. It presents the logic that tells us what action to take when a given condition is true or otherwise. *Decision tree:* A graphic representation of the conditions and outcomes that resemble the branches of a tree.

*Warnier/Orr diagrams:* A horizontal hierarchy chart using nested sets of braces, pseudo-codes, and logic symbols to indicate the program structure.

## 17.4 Object-Oriented Paradigm

The object-oriented paradigm draws heavily on the general systems theory as a conceptual background. A system can be viewed as a collection of *entities* that interact together to accomplish certain objectives (Fig. 17.3). Entities may represent physical objects such as equipment and people, and abstract concepts such as data files and functions. In object-oriented analysis, the entities are called *objects*.

PROCESS

![](img/62b7c32e48e4f960a8dc2825a7119fb2_688_0.png)

**Fig. 17.3** *A system showing inter-relationship of entities*

As the name indicates, the object-oriented paradigm places greater emphasis on the objects that encapsulate data and procedures. They play the central role in all the stages of the software development and, therefore, there exists a high degree of overlap and iteration between the stages. The entire development process becomes evolutionary in nature. Any graphical representation of the object-oriented version of the software development life cycle must, therefore, take into account these two aspects of overlap and iteration. The result is a “fountain model” in place of the classic “water-fall” model as shown in Fig. 17.4. This model depicts that the development reaches a higher level only to fall back to a previous level and then again climbing up.

![](img/62b7c32e48e4f960a8dc2825a7119fb2_689_0.png)

**Fig. 17.4** *Fountain model of object-oriented software development*

*Object-oriented analysis* (OOA) refers to the methods of specifying requirements of the software in terms of real-world objects, their behaviour, and their interactions. *Object-oriented design* (OOD), on the other hand, turns the software requirements into specifications for objects and derives class hierarchies from which the objects can be created. Finally, *object-oriented programming* (OOP) refers to the implementation of the program using objects, in an object-oriented programming language such as C++.

By developing specifications of the objects found in the problem space, a clear and well-organized statement of the problem is actually built into the application. These objects form a high-level layer of definitions that are written in terms of the problem space. During the refinement of the definitions and the implementation of the application objects, other objects are identified. **Figure 17.5** illustrates the layers of the object specifications that result from this process.

![](img/62b7c32e48e4f960a8dc2825a7119fb2_690_0.png)

All the phases in the object-oriented approach work more closely together because of the commonality of the object model. In one phase, the problem domain objects are identified, while in the next phase additional objects required for a particular solution are specified. The design process is repeated for these implementation-level objects.

In contrast to the traditional top-down functional decomposition approach, the object-oriented approach has many attributes of both the top-down and bottom-up designs. The top functional decomposition techniques can be applied to the design of individual classes, while the final system can be constructed with the help of class modules using the bottom-up approach.

## 17.5 Object-Oriented Notations and Graphs

Graphical notations are an essential part of any design and development process, and object-oriented design is no exception. We need notations to represent classes, objects, subclasses, and their inter-relationships. Unfortunately, there are no standard notations for representing the objects and their interactions. Authors and researchers have used their own notations. Some of them are used more frequently while others are not. Figures 17.6 through 17.14 show some of the commonly used notations to represent the following:

- 1. Classes and objects.
- 2. Instances of objects.
- 3. Message communication between objects.
- 4. Inheritance relationship.
- 5. Classification relationship.
- 6. Composition relationship.
- 7. Hierarchical chart.
- 8. Client-server relationship.
- 9. Process layering.

We must use these notations and graphs wherever possible. They improve not only the clarity of the processes but also the productivity of the software developers.

![](img/62b7c32e48e4f960a8dc2825a7119fb2_691_0.png)

*Fig. 17.6* Various forms of representation of classes/objects
