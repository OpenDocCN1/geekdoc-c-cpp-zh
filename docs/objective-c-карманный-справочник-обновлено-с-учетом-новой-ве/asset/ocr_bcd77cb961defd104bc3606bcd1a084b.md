# CHAPTER 1: The Objective-C Philosophy

**Note:** Objective-C also has a sister language, Objective-C++, which has the same relationship to C++ that Objective-C has to C. Objective-C++ is a pure superset of C++ and allows you to call C++ code from Objective-C objects, and vice versa. Because they have very different object models, you cannot subclass an Objective-C class with C++, or the converse; however, you can use pointers to Objective-C objects as fields in C++ objects and pointers to C++ objects as instance variables in Objective-C objects.

You can see this in the Cocoa frameworks. Not everything is an object. If you ask for a range of characters in a string, you will use NSRange structure. This is a C structure—not an Objective-C object—containing a location and a length. Points, rectangles, and several other things are represented in a similar way. If these were objects, then you would use more memory, make manipulating them slower, and not really gain any flexibility.

The Ingalls test^2 says that you should be able to create a new kind of integer and use this in positioning a window on the screen. Objective-C fails this test, but it's not a very useful example in the real world, because most of the time designing new kinds of

> ^2Named after Dan Ingalls, one of the designers of Smalltalk, who proposed it.