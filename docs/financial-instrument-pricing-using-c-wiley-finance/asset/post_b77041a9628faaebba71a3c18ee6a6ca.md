
- *Proxy* (an object that is a surrogate/placeholder for another object to control access to it).
- *Behavioural*: these are patterns that are concerned with inter-object communication, in particular the implementation of *algorithms* and the sharing of responsibilities between objects. These patterns describe run-time control and data flow in an application. We can further partition these patterns as follows:
  - *Variations*: patterns that customise the methods of a class in some way. In general, these patterns externalise the code that implements member functions. The main patterns are:
  - *Strategy* (families of interchangeable algorithms).
  - *Template Method* (defines the skeleton of an algorithm in a base class; some variant steps are delegated to derived classes; common or *invariant* functionality is defined in the base class).
  - *Command* (encapsulates a request as an object; execute the command).
  - *State* (allows an object to change behaviour when its internal state changes).
  - *Iterator* (provides a means to access the elements of an aggregate object in a sequential way without exposing its internal representation).
- *Notifications*: these patterns define and maintain dependencies between objects:
  - *Observer* (defines a one-to-many dependency between a *publisher* and its dependent subscribers).
  - *Mediator* (defines an object that allows objects to communicate without being aware of each other; this pattern promotes *loose coupling*).
  - *Chain of Responsibility* (avoids coupling between *sender* and *receiver* objects when sending requests; gives more than one object a chance to handle the request).
- *Extensions*: patterns that allow us to add new functionality (in the form of member functions) to classes in a class hierarchy. There is only one such pattern in GOF (1995):
  - *Visitor* (defines a new operation on the classes in a class hierarchy in a non-intrusive way).

There are some other, somewhat less universal behavioural patterns in GOF (1995):

- *Memento* (captures and externalises an object’s internal state so that it can be restored later).
- *Interpreter* (given a language, defines a representation for its grammar and defines an interpreter to interpret sentences in the language).

Which GOF patterns are useful when developing applications? An initial answer is that 20% of the design patterns are responsible for 80% of developer productivity in our experience. Many applications have similar characteristics and having determined what these characteristics are, we will be in a position to determine which design patterns to use. In general, application development involves the following activities:

- A1: Using *structural patterns* to compose classes and class hierarchies. In particular, we can extend the functionality of a class using inheritance and composition. The top three patterns are *Adapter*, *Composite* and *Decorator*.
- A2: Using *behavioural patterns* to extend and/or modify the classes in activity A1. On the one hand we may wish to extend the functionality of a class hierarchy (using the *Visitor* pattern), create flexible algorithms in single classes (*Strategy*) and in class hierarchies
(Template Method pattern). We also wish to keep objects in object networks consistent and in this case we could apply the Observer pattern, although its implementation as described in GOF (1995) is based on OOP (it is not even wrong) and a better solution is to use a signals-based approach (as described in Demming and Duffy, 2010) or to use .NET delegates which we shall describe in Chapter 27. For example, much of the functionality of the Observer pattern is realised by the .NET Event pattern.
- A3: Once we know which structural and behavioural patterns to use, we implement them using classes and objects. We also describe the structural relationships between these classes and objects. Of course, we instantiate these classes and this process must be customisable to allow us to instantiate classes in different ways and as flexibly as possible. To this end, we use creational patterns such as Factory Method (for specific classes), Abstract Factory (for inter-related classes and class hierarchies) and Builder (for configuring all objects in a complete application).

## 22.6.3 Patterns: Incremental Improvements

It is possible to upgrade the GOF patterns in a number of ways:

- S1: Keep and use the patterns in their current form without change.
- S2: Improve the patterns by using new improved C++ functionality such as shared pointers and the syntax that we discussed in the first 10 chapters of this book. These are relatively small improvements.
- S3: Re-engineer those patterns that can be implemented more easily and correctly using generic and functional programming models, for example.
- S4: Do not (yet) use design patterns but instead postpone their use in the design trajectory for as long as possible. Instead, we use the system decomposition techniques of Chapter 9 and hope to achieve the same (and possible improved) levels of flexibility as with GOF patterns but then by other means, specifically by defining standardised interfaces between components.

In general, we make a distinction between legacy software systems which may need to be upgraded and those systems that we design from scratch. In the former case the upgrade policies S1 and S2 might be appropriate while policy S3 is a possibility for design patterns that have been well designed and for which an upgrade has minimal impact on the stability of the software system. In the latter case we have the most freedom and we can choose the most appropriate design pattern (or combination of patterns) to satisfy our requirements.

## 22.7 MULTIPARADIGM DESIGN PATTERNS

In this book we discuss new C++ features that did not exist when the GOF patterns were born. We can speculate on whether these patterns were created in order to resolve some of the shortcomings in the language at the time of birth or whether they are indeed robust design techniques that can be reused in a variety of applications. Some patterns have fallen into disrepair, while others can be upgraded to give them a new lease of life. Yet others will be discovered that could not have been envisaged in GOF (1995).

We mention and introduce several design patterns as we progress in this book. We now give an overview of the top C++ features (in our opinion) that help upgrade design patterns. We also give some pointers on the features in the context of use cases S2 and S3.

- **Shared and unique pointers:** the original GOF patterns used raw pointers. Using smart pointers leads to more robust and reliable code.
- **Tuples:** provide the ability to group a collection of heterogeneous data as a single entity. They are particularly useful as part of the *Abstract Factory* and *Builder* patterns. The return type is a tuple of newly created objects. The GOF pattern interface has an abstract factory method for each product. Similarly, we can extend the *Builder* pattern to return a tuple whose elements can be created by *subcontractors*. At the moment we do not see many uses for tuples in improving structural and behavioural patterns. This may change as new applications for tuples are discovered.
- **Universal function wrappers** (`std::function`): these are abstract functions that can be ‘instantiated’ by assigning them to a *target method* of a callable object, for example. These are in fact polymorphic functions and using this fact allows us to reduce the number of derived classes that need to be created in patterns such as *Command*, *Strategy*, *Template Method* and *Observer*. This approach reduces the number of classes in an application and hence improves maintainability (see metrics M13 and M12 of Section 7.6.4).
- **Boost signals2:** this library supports *signals and slots* and is superior to the *Observer* and *Chain of Responsibility* patterns. Using class hierarchies to emulate events is somewhat of a fudge in our opinion.
- **Lambda functions** and stored lambda functions: these functions avoid our having to create classes and free functions, thus reducing drudgery and maintenance costs. These functions are most useful when developing code for creational patterns.
- **Variadic templates** and *variadic functions*: these features help to reduce code bloat. In the first case we only need to define a template class once and instantiate it many times while in the second case we only need to define a function with variadic arguments once.

A full discussion of these topics is outside the scope of this book and they will be discussed in a forthcoming work.

## 22.8 SUMMARY AND CONCLUSIONS

In this chapter we discussed how to compute some option sensitivities, notably delta and gamma. These are used for *hedging*. This is the reduction of risk by exploiting relationships between various risky investments. *Delta hedging* involves the perfect elimination of all risk by defining a hedge between an option and its underlying. *Gamma hedging* is used to reduce the size of each hedge which then results in a cost reduction. It is a more accurate form of hedging than delta hedging. In this chapter we discussed methods to compute these quantities.

## 22.9 EXERCISES AND PROJECTS

- 1. (Interpolation)
  Create C++ code to perform linear interpolation. Test the code in the same style as the code in Section 22.2. Display the results in Excel. Compare the results with those produced by cubic spline interpolation in Section 22.2.
- 2. (Automated FDM Tester, Medium-Sized Project)
  The objective of this exercise is to develop a *proof-of-concept* software framework to test the accuracy, robustness and run-time performance of a given finite difference scheme.
