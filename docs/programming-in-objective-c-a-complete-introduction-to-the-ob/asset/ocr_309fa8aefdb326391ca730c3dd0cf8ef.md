# Archiving with NSKeyedArchiver

the stringWithContentsFile: method. Program 19.2 reads back the glossary written
in Program 19.1 and displays its contents.

Program 19.2

```
#import <Foundation/Foundation.h>

int main (int argc
```

# Program 19.2 Output

archiving: Storing an object for later use.
abstract class: A class defined as other classes can inherit from it.
adopt: To implement all methods defined in a protocol

Your properties list don't need to be created from an Objective-C program; the prop-
erty can come from any source. You can make your own property lists using a simple
editor, or you can use the List Editor program located in the
/Developer/Applications/Utilities directory on Mac OS systems. If you plan to
work with property lists in your applications, you may want to take a look at the
PropertyListSerialization class, which allows property lists to be written to
read from files in a machine-portable format.

# Archiving with NSKeyedArchiver

A flexible approach enables you to save any type of objects to a file, not just strings,
arrays, and dictionaries. This is done by creating a keyed archive using the
NSKeyedArchiver class.

Mac OS has supported keyed archives since version 10.2. Before that, sequential
archives were created with the NSNSArchiver class. Sequential archives require that the data
in the archive be read back in the same order in which it was written.
A keyed archive is used in which each field of the archive has a name. When you
archive an object, you give it a name, or key. When you retrieve it from the archive, you
retrive it by the same key. In that, objects can be written to the archive and
retrieved in any order. Furthermore, if instance variables are added or removed to a
class, your program can account for it.