directory, it searches for it in the same location(s) as the C++ Standard Library headers. When the preprocessor encounters a header name in angle brackets (e.g., `<iostream>`), it assumes that the header is part of the C++ Standard Library and does not look in the directory of the file being preprocessed.

![](bbox=[0.159, 0.197, 0.216, 0.239])

> **Error-Prevention Tip 3.3**
> 
> *To ensure that the preprocessor can locate headers correctly, `#include` preprocessor directives should place user-defined headers names in quotes (e.g., "GradeBook.h") and place C++ Standard Library headers names in angle brackets (e.g., `<iostream>`).*

# *Additional Software Engineering Issues*

Now that class GradeBook is defined in a header, the class is reusable. Unfortunately, placing a class definition in a header as in Fig. 3.9 still reveals the entire implementation of the class to the class clients—GradeBook.h is simply a text file that anyone can open and read. Conventional software engineering wisdom says that to use an object of a class, the client code needs to know only what member functions to call, what arguments to provide to each member function and what return type to expect from each member function. *The client code does not need to know how these functions are implemented.*

If client code does know how a class is implemented, the programmer might write client code based on the class’s implementation details. Ideally, if that implementation changes, the class’s clients should not have to change. *Hiding the class’s implementation details makes it easier to change the class’s implementation while minimizing, and hopefully eliminating, changes to client code.*

In Section 3.7, we show how to break up the GradeBook class into two files so that

+   1. the class is *reusable*,
+   2. the clients of the class know what member functions the class provides, how to call them and what return types to expect, and
+   3. the clients do *not* know how the class’s member functions are implemented.

# 3.7 Separating Interface from Implementation

In the preceding section, we showed how to promote software reusability by separating a class definition from the client code (e.g., function `main`) that uses the class. We now introduce another fundamental principle of good software engineering—*separating interface from implementation.*

# *Interface of a Class*

Interfaces define and standardize the ways in which things such as people and systems interact with one another. For example, a radio’s controls serve as an interface between the radio’s users and its internal components. The controls allow users to perform a limited set of operations (such as changing the station, adjusting the volume, and choosing between AM and FM stations). Various radios may implement these operations differently—some provide push buttons, some provide dials and some support voice commands. The interface specifies *what* operations a radio permits its user to perform but does not specify *how* the operations are implemented inside the radio.