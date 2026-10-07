the data area; then you have to create an NSKeyedUnarchiver object and tell it to decode data from the specified area.You must invoke decode to extract and your archived objects. When you're finished, you send a finishDecoding message to the NSKeyedUnarchiver object.
This is all done in Program 19.10.

# Program 19.10

```
#import "AddressBook.h"
#import "Foo.h"

int main (int argc, char *argv[]) {
{
    NSAutorePool *pool = [NSAutorePool alloc init];
    NSData *dataArea;
    NSKeyedUnarchiver *unarchiver;
    Foo *myFoo;
    AddressBook *myBook;
    // Read the archive and connect an
    NSKeyedUnarchiver object to it

dataArea = [NSData dataWithContentsFile:@"myArchive"];

if (!dataArea) {
    NSLog("Can't read back archive file!");
    return 1;
}

unarchiver = [[NSKeyedUnarchiver alloc]
initForReadingWithData:dataArea];

// Decode the objects we previously stored in the archive
myBook = [unarchiver decodeObjectForKey"myaddbook"];
myFoo = [unarchiver decodeObjectForKey"myfoo"];

[unarchiver finishDecoding];

[unarchiver release];

// Verify that the restore was successful
[myBook list];
NSLog("%%@\n%n%@", [myBook strVal], [myFoo floatVal]);

[pool release];
return 0;
}
```

# Program 19.10 Output

Contents of: Steve's Address Book
Jamie Baker jbaker@hitmail.com
Julia Kochan jewls337@axlc.com
Stephen Kochan steve@steve.kochan.com
Tony Iannino tony.iannino@techfitness.com