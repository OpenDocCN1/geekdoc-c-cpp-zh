
## Simple Association

![](img/e143b38d00f95425fa4f3efca0527189_41_0.png)

- In an association Class A 'uses' objects of Class B
- Typically Class A has an attribute of Class B
- Navigability is from A to B:
  i.e. Class A object can access the Class B object(s) with which it is associated. The reverse is not true – the Class B object doesn't 'know' about Class A object

A simple association typically corresponds to an instance variable in Class A of the target class B type.

Example: the Catalogue above needs access to 0 or more ItemForSale so items can be added or removed from a Catalogue. An ItemForSale does not need to access a Catalogue in order to set its price or perform some other method associated with the item itself.

## Bidirectional Association

![](img/e143b38d00f95425fa4f3efca0527189_41_1.png)

- Bidirectional Association is when Classes A and B have a two-way association
- Each refers to the other class
- Navigability to A and B to A:
  - A Class A object can access the Class B object(s) with which it is associated
  - Object(s) of Class B 'belong' to Class A
  - Implies reference from A to B
  - Also, a Class B object can access the Class A object(s) with which it is associated

A bidirectional association is complicated because each object must have a reference to the other object(s) and generally bidirectional associations are much less common than unidirectional ones.

An example of a bidirectional association may be between a 'Degree' and 'Student'. i.e. given a Degree we may wish to know which Students are studying on that Degree. Alternatively starting with a student we may wish to know the Degree they are studying.

## Object Oriented Programming using C#

## The Unified Modelling Language (UML)

![](img/e143b38d00f95425fa4f3efca0527189_42_0.png)

As many students study the same Degree at the same time, but students usually only have one Degree there is still a one to many relationship here (of course we could model a situation where we record degrees being studied and previous degrees passed – in this case, as a student may have passed more than one degree, we would have a many to many relationship).

## Aggregation

![](img/e143b38d00f95425fa4f3efca0527189_42_1.png)

- Aggregation denotes a situation where Object(s) of Class B 'belong to' Class A
- Implies reference from A to B
- While aggregation implies that objects of Class B belong to objects of Class A it also implies object of Class B retain an existence independent of Class A. Some designers believe there is no real distinction between aggregation and simple association

![](img/e143b38d00f95425fa4f3efca0527189_42_2.png)

## Object Oriented Programming using C#

## The Unified Modelling Language (UML)

An example of aggregation would be between a class Car and a class Tyre

![](img/e143b38d00f95425fa4f3efca0527189_43_0.png)

We think of the tyres as belonging to the car they are, but at the garage they may be removed and placed on a rack to be repaired. Their existence isn't dependent on the existence of a car with which they are associated. Some designers believe that aggregation can be replaced as a simple association as when implementing this design in a program makes no difference to the programmer.

## Composition

![](img/e143b38d00f95425fa4f3efca0527189_43_1.png)

- Composition is similar to aggregation but implies a much stronger belonging relationship i.e. Object(s) of Class B are ‘part’ of Class A object
- Again implies reference from A to B
- Much ‘stronger’ than aggregation in this case Class B objects are an integral part of Class A and in general objects of Class B never exist other than part of Class A, i.e. they have the same ‘lifetime'

An example of composition would be between Points, Lines and Shapes as elements of a Picture. These objects can only exist as part of a picture, and if the picture is deleted they are also deleted.

As well as denoting associations, class diagrams can denote :-

- Inheritance,
- Interfaces,
- Keywords and
- Notes

Object Oriented Programming using C#

The Unified Modelling Language (UML)

## Inheritance

![](img/e143b38d00f95425fa4f3efca0527189_44_0.png)

- Aside from associations, the other main modelling relationship is inheritance:
- Class A ‘inherits’ both the interface and implementation of Class B, though it may override implementation details and supplement both.

We will look at inheritance in detail in Chapter 3.

## Interfaces

- Interfaces are similar to inheritance however with interfaces only the interface is inherited. The methods defined by the interface must be implemented in every class that implements the interface.
- Interfaces can be represented using the <<interface>> keyword:

![](img/e143b38d00f95425fa4f3efca0527189_44_1.png)

There is also a shorthand for this

![](img/e143b38d00f95425fa4f3efca0527189_44_2.png)

In both cases these examples denote that the SaleableItem interface is required by CashTill and implemented by Publication.

NB the dotted-line version of the inheritance line/arrow which shows that Publication ‘implements’ or ‘realizes’ the SaleableItem interface.

## Object Oriented Programming using C#

## The Unified Modelling Language (UML)

The “ball and socket” notation is new in UML 2 – it is a good visual way of representing how interfaces connect classes together.

We will look at the application of interfaces in more detail in Chapter 4.

## Keywords

UML defines keywords to refine the meaning of the graphical symbols We have seen <<interface>> and we will also use <<abstract>> but there are more.

An abstract class may be denoted by italics rather than the <<abstract>> keyword.

A customer can have any number of bank accounts, and a bank account can be held by one person or two people (“joint account”). We suppressed the navigability of this relationship, perhaps because we have not yet decided this issue.

(The text regarding "months of full-time" and "london.edu" appears to be corrupted/noise in the source OCR and has been cleaned to maintain logical flow).

Object Oriented Programming using C#

The Unified Modelling Language (UML)

## Notes

![](img/e143b38d00f95425fa4f3efca0527189_46_0.png)

Finally we can add notes to comment on a diagram. This gives us a 'catch-all' facility for adding information

## Activity 4

From your own experience, try to develop a model which illustrates the following elements:

- simple association
- bidirectional association
- aggregation (tricky!)
- composition
- multiplicity
- generalization (inheritance)
- interfaces
- notes

To help you get started some small examples are below:-
