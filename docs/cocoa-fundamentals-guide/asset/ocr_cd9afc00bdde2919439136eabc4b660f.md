# CHAPTER 4

Cocoa Design Patterns

> Further Reading: For further information on delegation, see "Delegates and Data Sources" (page 176).

# Categories

A category is a feature of the Objective-C language that enables you to add methods (interface and implementation) to a class without having to make a subclass. There is no runtime difference—within the scope of your program—between the original methods of the class and the methods added by the category. The methods in the category become part of the class and are inherited by all subclasses.

As delegation, categories are not a strict adaptation of the Decorator pattern, fulfilling the intent but taking a different path to implementing that intent. The behavior added by categories is a compile-time artifact, and is not something dynamically acquired. Moreover, categories do not encapsulate an instance of the class being extended.

# Uses and Limitations

The Cocoa framework defines numerous categories, most of them informal protocols (which are summarized in "Protocols" (page 140)). Often they use categories to group related methods. You may implement categories in your code without subclassing or to group related methods. However, you should be aware of these caveats:

+   - You cannot add instance variables to the class.

+   - If you override existing methods of the class, your application may behave unpredictably.

> Further Reading: See "Defining a Class" in The Objective-C Programming Language for more information on categories.

# Facade

The Facade design pattern provides a unified interface to a set of interfaces in subsystem. The pattern defines a higher-level interface that makes the subsystem easier to use by reducing complexity and hiding the communication and dependencies between subsystems.

# NSImage

The NSImage class of the AppKit framework provides a unified interface for loading and using images that can be bit-mapped (as those in JPEG, PNG, or TIFF format) or vector-based (as those in EPS or PDF format), NSImage can keep more than one representation of the same image; each representation is a kind of NSImageRep object. NSImage automates the choice of the representation that is appropriate for a particular type of data and for a given display device. It also holds the details of image manipulation and selection so that the client can use many different representations interchangeably.

How Cocoa Adapts Design Patterns
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.

147