```
myBook = [myBook initWithName: @"Steve's
Address Book
```

This program creates the address book and then archives it to the file addrbook.arch. In the process of creating the archive file, realize that the encoding methods from both the AddressBook and AddressCard classes were invoked. You can add some NSLog calls to these methods if you want proof.

Program 19.7 shows how you can read the archive into memory to set up the address book from a file.

# Program 19.7

```
#import "AddressBook.h"

int main (int argc, char * argv[])
```