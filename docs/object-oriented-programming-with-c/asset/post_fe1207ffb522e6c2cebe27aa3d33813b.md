
This process may be repeated at different levels of abstraction with the sole objective of extending the classes. As hierarchy structure becomes progressively higher, the amount of specification and implementation inherited by the lower level classes increases. We may repeat the process until we are sure that no new class can be formed. Figure 17.18 illustrates a two-level iteration process.

![](img/62b7c32e48e4f960a8dc2825a7119fb2_706_0.png)

The process of a class organization may finally result in a single-tree model as shown in Fig. 17.19(a) or forest model as shown in Fig. 17.19(b).

![](img/62b7c32e48e4f960a8dc2825a7119fb2_707_0.png)

(a) Single-tree model

(b) Forest model

**Fig. 17.19** *Organisation of classes*

## Design of Classes

We have identified classes, their attributes, and *minimal* set of operations required by the concept a class is representing. Now we must look at the complete details that each class represents. The important issue is to decide what functions are to be provided. For a class to be useful, it must contain the following functions, in addition to the service functions:

- 1. Class management functions.
  - How an object is created?
  - How an object is destroyed?
- 2. Class implementation functions.
  - What operations are performed on the data type of the class?
- 3. Class access functions.
  - How do we get information about the internal variables of the class?
- 4. Class utility functions.
  - How do we handle errors?

Other issues that are to be considered are:

- 1. What kind of access controls are required for the base classes?
- 2. Which functions can be made virtual?
- 3. What library classes are expected to be used in a class?
- 4. The design of the individual classes has a major impact on the overall quality of the software.

Given below are some guidelines which should be considered while designing a class:

- 1. The public interface of a class should have only functions of the class.
- 2. An object of one class should not send a message directly to a member of another class.
- 3. A function should be declared public only when it is required to be used by the objects of the class.
- 4. Each function either accesses or modifies some data of the class it represents.
- 5. A class should be dependent on as few (other) classes as possible.
- 6. Interactions between two classes must be explicit.
- 7. Each subordinate class should be designed as a specialization of the base class with the sole purpose of adding additional features.
- 8. The top class of a structure should represent the abstract model of the target concept.

## Design of Member Functions

We have so far identified

- 1. classes and objects,
- 2. data members,
- 3. interfaces,
- 4. dependencies, and
- 5. class hierarchy (structure)

It is time now to consider the design of the member functions. The member functions define the operations that are performed on the object’s data. These functions behave like any other C function and therefore we can use the top-down functional decomposition technique to design them as shown in Fig. 17.20.

We may also apply the *structured design* techniques to each module. The basic structured techniques supported by C++ are shown in Fig. 17.21. We may implement them in any combination and in any order using one-entry, one-exit concept.

## Design of the Driver Program

Every C++ program must contain a **main()** function code known as the driver program. The execution of the program begins and ends here. The driver program is mainly responsible for:

- 1. receiving data values from the user,
- 2. creating objects from the class definitions,
- 3. arranging communication between the objects as a sequence of messages for invoking the member functions, and
- 4. displaying output results in the form required by the user.

All activities, including processing during the execution of the program, result from the mutual interactions of the objects. One major design decision to be made is the logical order of the message passing.

The driver program is the gateway to the users. Therefore, the design of user-system interface (USI) should be given due consideration in the design of the driver program. The system should be designed to be user-friendly so that users can operate in a natural and comfortable way.

**Fig. 17.20** *Top-down design of functions*

![](img/62b7c32e48e4f960a8dc2825a7119fb2_712_0.png)

Implementation includes coding and testing. Coding includes writing codes for classes, member functions and the main program that acts as a driver in the program. Coding becomes easy once a detailed design has been done with care.

No program works correctly the first time. So testing the program before using is an essential part of the software development process. A detailed test plan should be drawn as to what, when and how to test. The class interfaces and class dependencies are important aspects for testing. The final goal of testing is to see that the system performs its intended job satisfactorily.

## 17.9 Prototyping Paradigm

Most often the real-world application problems are complex in nature and therefore the structure of the system becomes too large to work out the precise requirements at the beginning. Some particulars become known and clear only when we build and test the system. After a large system is completed, incorporation of any feature that has been identified as “missing” at the testing or application stage might be too expensive and time consuming. One way of understanding the system design and its ramifications before a complete system is built is to build and test a working model of the proposed system. The model system is popularly known as a *prototype*, and the process is called *prototyping*. Since the object-oriented analysis and design approach is evolutionary, it is best suited for *prototyping paradigm* which is illustrated in Fig. 17.22.

A prototype is a scaled-down version of the system and may not have stringent performance criteria and resource requirements. Developer and customer agree upon certain “outline specifications” of the system and a prototype design is proposed with the outline requirements and available resources. The prototype is built and evaluated. The major interest is not in the prototype itself but in its performance which is used to refine the requirement specifications. Prototypes provide an opportunity to experiment and analyze various aspects of the system such as system structure, internal design, hardware requirements and the final system requirements. The benefits of using the prototype approach are:

- We can produce understandable specifications which are correct and complete as far as possible.
- The user can understand what is being offered.
- Maintenance changes that are required when a system is installed, are minimized.
- Development engineers can work from a set of specifications which have been tested and approved.

![](img/62b7c32e48e4f960a8dc2825a7119fb2_714_0.png)

Fig. 17.22 *Prototype paradigm*

Prototype is meant for experimenting. Most often it cannot be tuned into a product. However, occasionally, it may be possible to tune a prototype into a final product if proper care is taken in redesigning the prototype. The best approach is to throw away the prototype after use.

## 17.10 Wrapping Up

We have discussed various aspects of the object-oriented analysis and design. Remember, there is no one approach that is always right. You must consider the ideas presented here as only guidelines and use your experience, innovation and creativity wherever possible.

Following are some points for your thought and innovation:

- 1. Set clear goals and tangible objectives.
- 2. Try to use existing systems as examples or models to analyze your system.
- 3. Use classes to represent concepts.
- 4. Keep in mind that the proposed system must be flexible, portable, and extendable.
- 5. Keep a clear documentation of everything that goes into the system.
- 6. Try to reuse the existing functions and classes.
- 7. Keep functions strongly typed wherever possible.
- 8. Use prototypes wherever possible.
- 9. Match design and programming style.
- 10. Keep the system clean, simple, small and efficient as far as possible.

## Summary

- ☐ The classic system development life cycle most widely used for procedure-oriented development consists of following steps.
- Problem definition
