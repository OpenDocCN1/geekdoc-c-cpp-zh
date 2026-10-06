archiving: Storing an object for later use.
abstract class: A class defined so other classes can inherit from it.
adopt: To implement all the methods defined in a protocol

Your property lists don't need to be created from an Objective-C program; the property list can come from any source. You can make your own property lists using a simple text editor, or you can use the Property List Editor program located in the //Applications/Utilities directory on Mac OS X systems. If you plan to work with property lists in your applications, you may want to take a look at the NSPropertyListSerialization class, which allows property lists to be written to and read from files in a machine-portable manner.

# Archiving with NSKeyedArchiver

A more flexible approach enables you to save any type of objects to a file, not just strings, arrays, and dictionaries. This is done by creating a keyed archive using the NSKeyedArchiver class.

Mac X has supported keyed archives since version 10.2. Before that, sequential archives were created with the NSArchiver class. Sequential archives require that the data in the archive be read back in precisely the same order in which it was written.

A keyed archive is one in which each field of the archive has a name. When you archive an object, you give it a name, or key. When you retrieve it from the archive, you retrieve it by the same key. In that manner, objects can be written to the archive and retrieved in any order. Furthermore, if new instance variables are added or removed to a class, your program can account for it.