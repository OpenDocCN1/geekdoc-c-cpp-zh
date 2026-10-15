

service through a browser—these are quite portable, so you can run the same applications on different kinds of computers from anywhere in the world. Salesforce.com, Google, and Microsoft’s Office Live and Windows Live all offer SaaS.

## 1.9 Future of C++: Open Source Boost Libraries, TR1 and C++0x

Bjarne Stroustrup, the creator of C++, has expressed his vision for the future of C++. The main goals for the new standard are to make C++ easier to learn, improve library building capabilities, and increase compatibility with the C programming language.

Chapter 21 considers the future of C++—we introduce the Boost C++ Libraries, Technical Report 1 (TR1) and C++0x. The *Boost C++ Libraries* are free, open source libraries created by members of the C++ community. Boost has grown to over 70 libraries, with more being added regularly. Today there are thousands of programmers in the Boost open source community. Boost provides C++ programmers with useful, well-designed libraries that work well with the existing C++ Standard Library. The Boost libraries can be used by C++ programmers working on a wide variety of platforms with many different compilers. We overview the libraries included in TR1 and provide code examples for the “regular expression” and “smart pointer” libraries.

*Regular expressions* are used to match specific character patterns in text. They can be used to validate data to ensure that it is in a particular format, to replace parts of one string with another, or to split a string.

Many common bugs in C and C++ code are related to pointers, which we present in Chapter 8, Pointers and Pointer-Based Strings. *Smart pointers* help you avoid errors by providing additional functionality to standard pointers. This functionality typically strengthens the process of memory allocation and deallocation.

*Technical Report 1* describes the proposed changes to the C++ Standard Library, many of which are based on current Boost libraries. These libraries add useful functionality to C++. The C++ Standards Committee is currently revising the C++ Standard. The last standard was published in 1998. Work on the new standard, currently referred to as *C++0x*, began in 2003. The new standard is likely to be released in 2009. It will include changes to the core language and, most likely, many of the libraries in TR1.

## 1.10 Software Engineering Case Study: Introduction to Object Technology and the UML

Now we begin our study of object orientation. Chapters 1–7, 9 and 13 all end with a brief Software Engineering Case Study section in which we present a carefully paced introduction to object orientation. Our goal here is to help you develop an object-oriented way of thinking and to introduce you to the *Unified Modeling Language*™ (*UML*®)—a graphical language that allows people who design object-oriented software systems to use an industry-standard notation to represent them.

In this required section, we introduce basic object-oriented concepts and terminology. The optional sections in Chapters 2–7, 9 and 13 present an object-oriented design and implementation of the software for a simple automated teller machine (ATM) system. The Software Engineering Case Study sections at the ends of Chapters 2–7

- analyze a typical requirements specification that describes a software system (the ATM) to be built
- determine the objects required to implement that system
- determine the attributes the objects will have
- determine the behaviors these objects will exhibit
- specify how the objects interact with one another to meet the system requirements

The Software Engineering Case Study sections at the ends of Chapters 9 and 13 modify and enhance the design presented in Chapters 2–7. Appendix E contains a complete, working C++ implementation of the object-oriented ATM system.

Although our case study is a scaled-down version of an industry-level problem, we nevertheless cover many common industry practices. You’ll experience a solid introduction to object-oriented design with the UML. Also, you’ll sharpen your code-reading skills by touring the complete, carefully written and well-documented C++ implementation of the ATM.

### Basic Object Technology Concepts

We begin our introduction to object orientation with some key terminology. Everywhere you look in the real world you see objects—people, animals, plants, cars, planes, buildings, computers, monitors and so on. Humans think in terms of objects. Telephones, houses, traffic lights, microwave ovens and water coolers are just a few more objects we see around us every day.

We sometimes divide objects into two categories: animate and inanimate. Animate objects are “alive” in some sense—they move around and do things. Inanimate objects do not move on their own. Objects of both types, however, have some things in common. They all have attributes (e.g., size, shape, color and weight), and they all exhibit behaviors (e.g., a ball rolls, bounces, inflates and deflates; a baby cries, sleeps, crawls, walks and blinks; a car accelerates, brakes and turns; a towel absorbs water). We’ll study the kinds of attributes and behaviors that software objects have.

Humans learn about existing objects by studying their attributes and observing their behaviors. Different objects can have similar attributes and can exhibit similar behaviors. Comparisons can be made, for example, between babies and adults, and between humans and chimpanzees.

Object-oriented design (OOD) models software in terms similar to those that people use to describe real-world objects. It takes advantage of class relationships, where objects of a certain class, such as a class of vehicles, have the same characteristics—cars, trucks, little red wagons and roller skates have much in common. OOD takes advantage of inheritance relationships, where new classes of objects are derived by absorbing characteristics of existing classes and adding unique characteristics of their own. An object of class “convertible” certainly has the characteristics of the more general class “automobile,” but more specifically, the roof goes up and down.

to stand at attention), objects also communicate via messages. A bank account object may receive a message to decrease its balance by a certain amount because the customer has withdrawn that amount of money.

OOD *encapsulates* (i.e., wraps) attributes and *operations* (behaviors) into objects—an object’s attributes and operations are intimately tied together. Objects have the property of *information hiding*. This means that objects may know how to communicate with one another across well-defined *interfaces*, but normally they are not allowed to know how other objects are implemented—implementation details are hidden within the objects themselves. We can drive a car effectively, for instance, without knowing the details of how engines, transmissions, brakes and exhaust systems work internally—as long as we know how to use the accelerator pedal, the brake pedal, the steering wheel and so on. Information hiding, as we’ll see, is crucial to good software engineering.

Languages like C++ are *object oriented*. Programming in such a language is called *object-oriented programming (OOP)*, and it allows computer programmers to implement object-oriented designs as working software systems. Languages like C, on the other hand, are *procedural*, so programming tends to be *action oriented*. In C, the unit of programming is the *function*. In C++, the unit of programming is the *class* from which objects are eventually *instantiated* (an OOP term for “created”). C++ classes contain functions that implement operations and data that implements attributes.

C programmers concentrate on writing functions. Programmers group actions that perform some common task into functions, and group functions to form programs. Data is certainly important in C, but the view is that data exists primarily in support of the actions that functions perform. The *verbs* in a system specification help the C programmer determine the set of functions that will work together to implement the system.

### Classes, Data Members and Member Functions

C++ programmers concentrate on creating their own *user-defined types* called *classes*. Each class contains data as well as the set of functions that manipulate that data and provide services to *clients* (i.e., other classes or functions that use the class). The data components of a class are called *data members*. For example, a bank account class might include an account number and a balance. The function components of a class are called *member functions* (typically called *methods* in other object-oriented programming languages such as Java). For example, a bank account class might include member functions to make a deposit (increasing the balance), make a withdrawal (decreasing the balance) and inquire what the current balance is. You use built-in types (and other user-defined types) as the “building blocks” for constructing new user-defined types (classes). The *nouns* in a system specification help the C++ programmer determine the set of classes from which objects are created that work together to implement the system.

Classes are to objects as blueprints are to houses—a class is a “plan” for building an object of the class. Just as we can build many houses from one blueprint, we can instantiate (create) many objects from one class. You cannot cook meals in the kitchen of a blueprint; you can cook meals in the kitchen of a house. You cannot sleep in the bedroom of a blueprint; you can sleep in the bedroom of a house.

Classes can have relationships with other classes. For example, in an object-oriented design of a bank, the “bank teller” class needs to relate to other classes, such as the “customer” class, the “cash drawer” class, the “safe” class, and so on. These relationships are called *associations*.

