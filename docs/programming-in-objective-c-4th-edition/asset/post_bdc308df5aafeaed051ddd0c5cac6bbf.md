
delegate An object directed to carry out an action by another object.

designated initializer The method that all other initialization methods in the class, or in subclasses (through messages to super), will invoke.

dictionary A collection of key/value pairs implemented under Foundation with the NSMutableDictionary and NSMutableDictionary classes.

directive In Objective-C, a special construct that begins with at sign (@). @interface, @end, and @class are examples of directives.

Distributed Objects The capability of Foundation objects in one application to communicate with Foundation objects in another application, possibly running on another machine.

dynamic binding Determining the method to invoke with an object at runtime instead of compile time.

dynamic typing Determining the class to which an object belongs at runtime instead of compile time. See also static typing.

encapsulation See data encapsulation.

extern variable See global variable.

factory method See class method.

factory object See class object.

formal protocol A set of related methods grouped together under a name declared with the @protocol directive. Different classes (not necessarily related) can adopt a formal protocol by implementing (or inheriting) all its required methods. See also informal protocol.

forwarding The process of sending a message and its associated argument(s) to another method for execution.

Foundation framework A collection of classes, functions, and protocols that form the foundation for application development, providing basic facilities such as memory management, file and URL access, the tasks of archiving and working with collections, strings, and number and date objects.

framework A collection of classes, functions, protocols, documentation, and header files and other resources that are all related. For example, the Cocoa framework is used in developing interactive graphical applications under Mac OS X.

function A block of statements identified by a name that can accept one or more arguments passed to it by value and optionally return a value. Functions can be either local (static) to the file in they they are defined or global, in which case they can be called from functions or methods in other files.

garbage collection A runtime memory-management system that automatically releases the memory used by unreferenced objects. Garbage collection is not supported in the iOS runtime environment.

gcc The name of the compiler developed by the Free Software Foundation (FSF). gcc supports many programming languages, including C, Objective-C, and C++. gcc is the standard compiler used in Mac OS X for compiling Objective-C programs.

gdb The standard debugging tool for programs compiled with gcc.

getter method An accessor method that retrieves the value of an instance variable. See also setter method.

global variable A variable defined outside any method or function that can be accessed by any method or function in the same source file or from other source files that declare the variable as extern.

header file A file that contains common definitions, macros, and variable declarations that is included in a program using either an #import or an #include statement.

**id** The generic object type that can hold a pointer to any type of object.

**immutable object** An object whose value cannot be modified. Examples from the Foundation framework includes NSString, NSDictionary, and NSArray objects. See also mutable object.

**implementation section** The section of a class definition that contains the actual code (that is, implementation) for the methods declared in the corresponding interface section (or as specified by a protocol definition).

**informal protocol** A logically related set of methods declared as a category, often as a category, all the methods in an informal protocol do not have to be implemented. See also formal protocol.

**inheritance** The process of passing methods and instance variables from a class, starting with the root object, down to subclasses.

**instance** A concrete representation of a class. Instances are objects that are typically created by sending an alloc or new message to a class object.

**instance method** A method that can be invoked by an instance of a class. See also class method.

**instance variable** A variable declared in the interface section (or inherited from a parent) that is contained in every instance of the object. Instance methods have direct access to their instance variables.

**Interface Builder** A tool under Mac OS X for building a graphical user interface for an application.

**interface section** The section for declaring a class, its superclass, instance variables, and methods. For each method, the argument types and return type are also declared. See also implementation section.

**internationalization** See localization.

isa A special instance variable defined in the root object that all objects inherit. The *isa* variable is used to identify the class to which an object belongs at runtime.

**linking** The process of converting one or more object files into a program that can be executed.

**local variable** A variable whose scope is limited to the block in which it is defined. Variables can be local to a method, function, or statement block.

**localization** The process of making a program suitable for execution within a particular geographic region, typically by translating messages to the local language and handling things such as time zones, currency symbols, date formats, and so on. Sometimes *localization* is used just to refer to the language translation, and the term *internationalization* is used to refer to the rest of the process.

**message** The method and its associated arguments are sent to an object (the receiver).

**message expression** An expression enclosed in square brackets that specifies an object (the receiver) and the message to send to the object.

**method** A procedure that belongs to a class and can be executed by sending a message to a class object or to instances from the class. See also [class method]()[instance method].

**mutable object** An object whose value can be changed. Foundation framework supports mutable and immutable arrays, sets, strings, and dictionaries. See also [immutable object]().

nil An object of type id, which is used to represent an invalid object. Its value is defined as 0. nil can be sent messages.

notification The process of sending a message to objects that have registered to be alerted when a specific event occurs.

NSObject The root object under the Foundation.

null character A character whose value is 0. null character constant is denoted by '\0'.

null pointer An invalid pointer value, normally defined as 0.

object A set of variables and associated methods. An object can be sent messages to cause one of its methods to be executed.

object-oriented programming A method of programming based on classes and objects, and performing actions on these objects.

parent class A class from which another class inherits. Also referred to as the super class.

pointer A value that references another object or data type. A pointer is implemented as the address of a particular object. An instance of a class is a pointer to the location of the object in memory.

polymorphism The capability of objects from different classes to accept the same message.

procedural programming language A language in which programs are defined by procedures and functions that operate on a set of data.

property declaration A way to specify attributes for instance variables that enables the compiler to generate leak-free and thread-safe accessor methods for instance variables. Property declarations can also be used to declare attributes for accessor methods that will be dynamically loaded at runtime.

preprocessor A program that makes a first pass through the source code processing lines that begin with a #, which presumably contain preprocessor statements. Common uses are for defining macros with #define, including other source files with #import and #include, and conditionally including source lines with #if, #ifdef, and #ifndef.

property list A representation of different types of objects in a standardized format. Property lists are typically stored in XML format.

protocol A list of methods that a class must implement to conform or adopt the protocol. Protocols provide a way to standardize an interface across classes. See also formal protocol informal protocol.

receiver The object to which a message is sent. The receiver can be referred to as self inside the method that is invoked.

reference count See retain count.

retain count A count of the number of times an object is referenced. It's incremented by sending a retain message to the object, and it's decremented by sending a release message to it.

root object The topmost object in the inheritance hierarchy that has no parent.

runtime The time when a program is executing; also the mechanism responsible for executing a program's instructions.

selector The name used to select the method to execute for an object. Compiled selectors are of type SEL and can be generated using the @selector directive.
