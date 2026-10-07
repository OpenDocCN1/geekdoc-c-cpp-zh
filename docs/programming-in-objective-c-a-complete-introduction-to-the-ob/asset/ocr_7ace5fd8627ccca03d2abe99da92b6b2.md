[encoder encodeInt:intForKey:@@"FoointVal\];
[encoder encodeFloat:floatVal forKey::@@"FoofloatVal\];

Some of the basic data types, such as char, short, long, and long long, are not listed in Table 19.1; you must determine the size of your data object and assign it to the appropriate routine. For example, a short int is normal 16 bits, an int and a long can be 32 or 64 bits, and a long is 64 bytes. (Using the sizeof operator, described in Chapter 13,"Underlying C Language Features," to determine the size of your data type.) To archive a short int, store it in an int first and archive it with encodeIntForKey:
Reverse the process to get it back: Use decodeIntForKey and assign it to your short int value.

# UsingNSData to Create Custom Archives

You might not want to write your object directly to a file using the archiverRootObject:ToFile method, as was in the previous examples. For example, you may collect some or all of your objects and store them in a single file. You can do this in Objective-C using the data class NSData, which we briefly visited in Chapter 16,"Working with Files."

As mentioned in Chapter 16, an NSData object can be used to reserve an area of memory into which you can store data. Typical uses of this data area might be to provide temporary storage for data that will subsequently be written to a file or perhaps to hold the contents of a file read from the disk. The simplest way to create a mutable data area is

This creates an empty buffer whose size expands as needed as the program executes.
As a simple example, let's assume you want to archive your address book and one of your Foo objects in the same file. Assume for this example that you have added keyed methods to the AddressBook and AddressCard classes in Program 19.9.

Program 19.9

```
#import "AddressBook.h"
#import "Foo.h"

int main(int argc, char *argv[]) {
[NSAutleasePool [[NSAutleasePool alloc] init];
Foo *myFoo=[Foo alloc] init];
Data *dataArea=nil;
NSKeyedArchiver *archiver=nil;
AddressBook *myBook=nil;

// Insert code from Program 19.7 to create an Address Book
// in myBook containing four address cards

[myFoo setStringVar:@"This is the string\];
```