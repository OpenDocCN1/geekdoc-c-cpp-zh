
Figure 10.4 Basic UML symbols and notation

# Chapter 10 587

A Closer Look: Object Identification and the Unified Modeling Language (UML)

| U.S.A. |
| --- |
| North America 381 million |
| Country |
| --- |
| Continent Population |
| Object diagram |
| Spain |
| --- |
| Europe 34 million |

Figure 10.5 Including attributes in UML class and object diagrams

Visibility defines where an attribute can be seen—that is, whether the attribute is used in other classes or restricted to the class. The following list explains the types of visibility and the UML notation for indicating visibility:

- *Private*—An attribute with private visibility can be used only in its class and cannot be accessed by other classes directly. A minus sign (-) in front of the attribute name designates the attribute as private.
- *Public*—An attribute with public visibility can be used in any other class. Public visibility is indicated with a plus sign (+) in front of the attribute name.
- *Protected*—An attribute with protected visibility can be passed along to a derived class; neither a plus sign nor a minus sign is used to indicate protected visibility.

In a class diagram, an attribute's name and type are required; all other information is optional. Figure 10.6 illustrates the class diagram for a class *RoomType* containing two private attributes: length and width. Notice that it includes the default values the class is expected to provide to its attributes.

| RoomType |
| --- |
| -length : double = 25.0 |
| -width : double = 12.0 |

Figure 10.6 A class with attributes

As attributes are designated in a class diagram, so are operations. Operations are transformations that can be applied to attributes and are coded as C++ functions. Operation names are listed below attributes and separated from them by a line. Figure 10.7 shows two class diagrams that include operations.

# Introduction to Classes

| Person | Gas Pump |
| --- | --- |
| -name : string | -gallonsInTank : double |
| -street : string | -costPerGallon : double |
| -city : string | +enablePump () |
| -state : string | +disablePump () |
| -zip : string | +setPricePerGallon () |
| -age : double | |
| +setName () | |
| +setAddress () | |
| +setAge () | |
| +changeName () | |
| +changeAddress () | |
| +changeAge () | |

Figure 10.7 Including operations in class diagrams

# Relationships

In addition describing classes and objects, UML class and object diagrams show the relationships between classes and/or objects. The three basic relationships are association, aggregation, and generalization.

- Associations between classes are typically signified by phrases such as "is related to", "is employed by", "works for" and so forth. This relationship is indicated by a straight line connecting two classes or objects, and the type of association is listed above or below the line. For example, Figure 10.8 shows an association between a Person and a Company. As indicated, a Company "employs" zero or more Persons. The designation of "zero or more," referred to as the multiplicity of the relationship, is indicated by the * symbol in the diagram. Table 10.2 lists the symbols for indicating the multiplicity. These symbols can be placed above or below the line connecting two classes or objects.

| Company | employs * | Person |
| --- | --- | --- |

Figure 10.8 An association

Table 10.2 UML Association Notation

| Symbol | Relationship |
| --- | --- |
| 1 | One and only one |
| n | Exactly the specified number (n is integer) |
| 0..1 | Zero or one |
| m..n | From m to n (m and n are integers) |
| * or 0..* | From zero to positive integer |
| 1..* | From one to any positive integer

# Chapter 10 589
A Closer Look: Object Identification and the Unified Modeling Language (UML)

An aggregation is a type of composition in which one class or object, referred to as the whole element, "consists of" or "is composed of" other classes or objects, which are referred to as parts. For example, a sentence consists of words, which consist of characters. Therefore, characters are parts of words, which are parts of sentences. This relationship is indicated by a diamond symbol attached to the class or object representing the whole element. Figures 10.9, 10.10, and 10.11 illustrate three aggregation diagrams. It is easier if you replace the diamond with the words "consists of" or "is composed of". When the diamond symbol is hollow, as in Figure 10.9, it indicates that the parts can still exist independent of the whole to which they belong. In other words, even if the team is broken up or destroyed, its members can still exist.

| Team | 1.25 Member |
| --- | --- | --- |
| | (consists of) |

**Figure 10.9** Single-level aggregation

A solid diamond symbol, as in Figures 10.10 and 10.11, indicates that the component parts are intrinsic members of the whole. Therefore, if the whole class or object is removed, all its aggregate parts are also destroyed. As indicated in Figure 10.10, if a sentence is removed, all its associated words are removed. Similarly, erasing a word erases the characters in the word.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_608_0.png)

**Figure 10.10** Another single-level aggregation

The last type of relationship to consider is generalization, more commonly referred to as inheritance. **Inheritance** is a relationship between a class and a derived version of the class. For example, a derived version of the class Vehicle can be Land, Space, or Water. In this case, Vehicle is the base class, and Land, Space, and Water are the derived classes. Figure 10.12 shows a class diagram of this inheritance relationship.

# 590 Introduction to Classes

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_609_0.png)

Figure 10.11 Multilevel aggregation

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_609_1.png)

Figure 10.12 An inheritance relationship

# EXERCISES 10.4

- 1. (For Review) Define the following terms:
  a. Attribute
  b. Behavior
  c. Class
  d. Identity
  e. Model
  f. Object
  g. Object diagram
  h. State
  i. Value
  j. Operation

- 2. (For Review) Classify the following as classes or objects:
  a. Maple trees
  f. Your Ford Taurus
  b. Ford automobiles
  g. Kitchen tables
  c. My collie dog
  h. Student desks
  d. The oak tree in your neighbor's yard
  i. The chair you're sitting on
  e. Boeing 767 planes

- 3. (Practice) a. For each of the following, determine what attributes might be of interest to someone buying the item:
  i. A book
  ii. A can of soda
  iii. A pen
  iv. A CD/DVD
  v. A CD/DVD player
  vi. An elevator
  vii. A car
  b. For each of the following, determine what attributes might be of interest to someone buying the item:
  a. A computer
  b. A CD/DVD player
  c. An elevator

- 4. (Practice) For each of the following, determine what attributes might be of interest to someone buying the item:
  a. A car
  b. A CD/DVD player
  c. An elevator

- 5. (Practice) a. List attributes for a character in a video game.
  b. List behaviors that a character should have.

- 6. (Practice) a. List attributes and behaviors in a program that dealing playing cards. For this exercise, use any card you're familiar with.
  b. What attributes of cards wouldn't be of interest for purposes of simulation?

- 7. (Practice) a. List attributes and behaviors in a program intended to simulate elevator moving between 1st to 15th floors of a building.
  b. What attributes of the elevator wouldn't be of interest for purposes of simulation?

- 8. (Practice) Construct a class diagram for Country. Each country has a capital city. The attributes of interest for country are its population, size, main agricultural product, and main manufactured product.

- 9. (Practice) Construct a class diagram for a book consisting of one more chapters, each of which consists of one more sections.

# Introduction to Classes

- 10. (Practice) a. Construct a class diagram for computer that consists of a monitor, keyboard, mouse, and system box.
  b. Modify the class diagram constructed in 10a to denote that one or more monitors and keyboards might be attached to the system box, and the system might have multiple mice.
  c. Extend the class diagram for 10b to denote that the system box is composed of a CPU chip, a memory board containing zero or more RAM chips, and case.

- 11. (Practice) a. Construct a class diagram for single gas tank connected to one or more gas pumps. The attributes of interest for the tank are its capacity, current level, and grade of gas. The attributes of interest for pump are the number of gallons dispensed and the cost per gallon. A pump responds to being enabled and disabled.
  b. Modify the diagram constructed in 11a to denote that a gas pump can be associated with more than one gas tank.

- 12. (Practice) Construct a class diagram for class of circles that are the base class for class of spheres and class of cylinders.

- 13. (Practice) Construct a class diagram for collection of cards consisting of zero or more cards. The collection of cards forms a base class for both a deck of cards and a hand of cards.

- 14. (Practice) Determine a car's major subsystems, such as brakes, steering, and so forth. Considering these subsystems as classes, construct a class diagram for Car class that simply shows the associations between classes (no attributes or operations). Then determine a set of attributes and operations for each subsystem, and modify the original class diagram to include the additional information.

- 15. (Practice) Determine a cell phone's major subsystems, such as keypad, antenna, and so on. Considering these subsystems as classes, construct a class diagram for CellPhone class that simply shows the associations between classes (no attributes or operations). Then determine a set of attributes and operations for each subsystem, and modify the original class diagram to include the additional information.

# 10.5 Common Programming Errors

Some programming errors associated with constructing classes are as follows:

- 1. Failing to terminate the class declaration section with a semicolon.
- 2. Including a return type with the constructor's prototype or failing to include a return type with the other functions' prototypes.
- 3. Using the same name for a data member as a member function.
- 4. Defining more than one default constructor for a class.
- 5. Forgetting to include the class name and scope operator, ::, in the function header of all member functions defined in the class implementation section.

All these errors result in a compiler error message.
