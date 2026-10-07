# Basic Subclass Design

All subclasses, regardless of subclass share certain characteristics when they are well designed. A poorly designed subclass is susceptible to error, hard to use, difficult to extend, and a drag on performance. A well-designed subclass is quite the opposite. This section offers suggestions for designing subclasses that are efficient, robust, and both useful and reusable.

Although this document describes some of the mechanics of crafting a subclass, it focuses primarily on design. It does not describe how you can use the developments Xcode and Interface Builder to automate part of class definition. To learn about these applications, read A Tour of Xcode. The information presented in this section is particularly applicable to model objects. Model Object Implementation Guide discusses the proper design and implementation of model objects at length.

# The Form of a Subclass Definition

Objective-C class consists of an interface and an implementation. By convention, two parts of a class definition go in separate files. The name of the interface file (as ANSI C header files) has an extension of .h; the name of the implementation file has an extension of .m. The name of the file up to the extension is typically the name of the class. For a class named Controller, the files would be:

```
Controller.h
Controller.m
```

The interface file contains a list of property, method, and function declarations that establish the public interface of the class. It also holds declarations of instance variables, constants, string globals, and other data types. The @interface directive introduces the essential declarations of the interface, and the @end directive terminates the class. The @interface directive is particularly important because it identifies the name of the class and the class directly inherited from, using the form:

```
@interface own : Superclass
```

Listing 3-2 gives an example of the interface file for the hypothetical Controller class, before any declarations are made.

> Listing 3-2 The basic structure of an interface file
#import <Foundation/Foundation.h>

```
@interface Controller : NSObject {
}
@end
```

To complete the class interface, you must make the necessary declarations in the appropriate places in this interface structure, as shown in Figure 3-4.