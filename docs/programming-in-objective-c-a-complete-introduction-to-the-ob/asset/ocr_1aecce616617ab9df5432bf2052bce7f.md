# Archiving

Objective-C terms, archiving is the process of saving one or more objects in a format so that they can later be restored. Often this involves writing the object(s) to a file so it can subsequently be read. We discuss two methods for archiving data in this chapter: property lists and key-valued coding.

# Archiving with XML Property Lists

Mac OS X applications use XML properties (or plists) for storing things such as your default preferences, application settings, and configuration information, so it's useful to know how to create them and read back in. Their use for archiving purposes, however, is limited because creating a property list for a data structure, specific object classes are not retained, multiple references to the same object are not stored, and the mutability of an object is not preserved.

> Note
-called "old-style" property lists store the data in a different format than XML property lists. Stick to using XML property lists in your program, if possible.

If your objects are NSString, NSDictionary, NSArray, NSDate, NSData, or NSNumber, you can use the writeToFile:atomically: method implemented in these classes to write your data to a file. In the case of writing a dictionary or an array, this method writes the data to the file in the format of an XML property list. Program 19.1 shows how the dictionary you created as a simple glossary in Chapter 15, "Numbers, Strings, and Collections," can be written to a file as a property list.

19.1

```
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSDictionary *glossary =
    [NSDictionary dictionaryWithObjectsAndKeys:
        @"A class defined so other classes can inherit from it.",
```