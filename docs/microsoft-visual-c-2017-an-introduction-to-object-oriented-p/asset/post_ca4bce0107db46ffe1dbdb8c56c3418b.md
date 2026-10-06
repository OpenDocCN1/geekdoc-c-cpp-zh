
# CHAPTER 1 A First Program Using C#

speed or the Dog's shots, but you know that those attributes exist for the Automobile and Dog classes. Similarly, in a GUI operating environment, you expect each window you open to have specific, consistent attributes, such as a menu bar and a title bar, because each window includes these attributes as a member of the general class of GUI windows.

By convention, programmers using C# begin their class names with an uppercase letter and a singular noun. For example, the class that defines the attributes and methods of an automobile would probably be named Automobile, and the class that contains those would probably be named Dog. If the class requires two nouns, programmers conventionally use camel casing, as in BankAccount.

Besides attributes, objects possess methods that they use to accomplish tasks, including changing attributes and discovering the values of attributes. Automobiles, for example, have methods for moving forward and backward. They can also be filled with gasoline or washed; both methods are the same of an Automobile's attributes. Methods also exist for determining the status of certain, such as the current speed of an Automobile and the number of gallons of gas in its tank. Similarly, a Dog can walk or run, eat, and get a bath; and there are methods for determining whether it needs water, food, or a bath. GUI operating system components, which can be maximized, minimized, and dragged; depending on the component, they can also have their color or font styled.

Like procedural programs, object-oriented programs encapsulate variables (attributes) and procedures (methods), where attributes and methods are encapsulated into objects that are used much like real-world objects. Encapsulation is the technique of packaging an object's attributes and methods into a cohesive unit that can be used as an undivided entity. Programmers sometimes refer to encapsulation as a black box, device you use without regard for the internal mechanisms. If an object's methods are well written, you are unaware of the level details about how the methods are executed; in such a case, the user must understand only the interface or interaction between the method and object. For example, if you can fill your Automobile with gasoline, you only need to understand the interface between the gas nozzle and the vehicle's gas tank opening. You don't need to understand how the pump works or where the gas tank is inside your vehicle. If you can read your speedometer, it does not matter how the display value is calculated. If, fact someone produces a new, accurate speedometer and inserts it into your Automobile, you don't have to know how it operates, as long as the interface remains the same as the previous one. The same principles apply to well-constructed objects used in object-oriented programs.

Object-oriented programming languages support two distinguishing features in addition to organizing objects as classes. One feature, inheritance, provides the ability to extend a class to create a more specific class. The more specific class contains all the attributes and methods of the more general class and usually contains new attributes and methods as well. If you have created a Dog class, you might create a more specific class ShowDog. Each instance of the ShowDog class would contain, or inherit, all the attributes and methods of a Dog, along with additional methods or attributes. For example, a ShowDog might require an attribute to hold the number of ribbons won and a method for extending its age. The advantage of inheritance is that when you need a class you can extend an existing class, saving a lot of time and work.

# The C# Programming Language

Object-oriented languages support polymorphism, which is the ability to create methods that act appropriately depending on the context. That is, programs written in object-oriented languages can distinguish between methods with the same name based on the type of object they use. For example, you are able to "fill" a Dog and an Automobile so by different means. Similarly, the procedure to "fill" a ShowDog might require different food than for a "plain" Dog. Old, non-object-oriented languages could not make such distinctions, object-oriented languages can.

The chapters "Using Classes and Objects" and "Introduction to Inheritance" contain much more information about the features of object-oriented programs.

Watch the video Object-Oriented Programming.

# TWO TRUTHS & A LIE
Features of Object-Oriented Programming Languages

- 1. Object-oriented programs contain classes that describe the attributes and methods of objects.
- 2. Object-oriented programming languages support inheritance, which refers to the packaging of attributes and methods into logical units.
- 3. Object-oriented programming languages support polymorphism, which is the ability of a method to act appropriately in the context.

Encapsulation refers to the packaging of attributes and methods. The false statement is #2. Inheritance is the ability to extend classes to make specific ones.

# The C# Programming Language

The C# programming language was developed as an object-oriented and component-oriented language. It is part of Microsoft Visual Studio, a package designed for developing applications that run on Windows computers. (The newest version of C# is 7.0; the version number tells you six major versions prior to the most recent.) Unlike other programming languages, C# allows every piece of data to be treated as an object and to consistently employ the principles of object-oriented programming. C# provides constructs for creating components with properties, methods, and events, making it an ideal language for modern programming, where small, reusable components are more important than building huge, stand-alone applications. You can find Microsoft's C# specifications at mdn.microsoft.com. Search for C# specifications.

If you have not programmed before, the differences between C# and other languages mean little to you. However, experienced programmers will appreciate the thought that was put into C# features. For example:

- C# has a GUI interface that makes it similar to Visual Basic, but C# is considered more concise than Visual Basic.
- C# is modeled after the C++ language, but is considered easier to learn. Most of the most difficult features to understand in C++ have been eliminated in C#.

- Some differences between C and C++ are that variables (that hold memory addresses) are not used in C# (except in a mode called unsafe, which is rarely used), destructors and forward declarations are not needed, and using #include files is not necessary. Multiple inheritance, which causes C++ programming errors, is not allowed in C#.

> In Java

The C# programming language was standardized in 2002 by Ecma International. You can read or download this set of standards at www.ecma-international.org/publications/standards/Ecma-334.htm.

| TWO TRUTHS & A LIE | The C# Programming Language |
| 1. The C# programming language was developed as an object-oriented and component-oriented language. |
| 2. C# contains several features that make it similar to other languages such as Java and Visual Basic. |
| 3. C# contains many advanced features, so the C++ programming language was a simpler version of the language. |

The false statement is 3. C# is modeled after C++ so some of the most difficult features to understand in C++ have been eliminated in C#.
