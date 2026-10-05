This represents the is-a relationship.

+   - Interface
The communication interface of your program to the outside.

+   - Messages
Objects communicate with each other by sending messages to their respective interfaces. In C++, they call methods of other objects for this purpose.

+   - Object
A closed unit of data and behavior—in C++, the instance of a class. In OOP, the data of objects are often called *fields* or *attributes*. The behavior is defined in C++ using methods on the class or free functions—OOP calls these both *procedures*.

+   - Polymorphism
The ability of a program to behave differently with different objects.

+   - Modularization
More manageable units of the program through abstraction and division into classes.

The motivation for OOP is the better reusability of programs or modules. Abstraction should help solve problems that have already been solved with the same program code. For this to work, clean encapsulation and information hiding are necessary to minimize dependencies between program parts.

Instead of changing the individual bits and bytes of a large global state while programming, you take a step back by sending messages and look at the bigger