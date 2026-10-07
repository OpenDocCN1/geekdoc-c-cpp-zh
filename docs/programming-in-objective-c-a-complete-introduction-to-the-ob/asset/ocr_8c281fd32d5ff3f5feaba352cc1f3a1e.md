# Array Objects

Returning Program 15.8, the print method tries to present the user with a nice display of an address card in a format resembling a Rolodex card (anyone remember those?). The %-31s characters NSLog indicate a display UTF-8 C-string in a field width of 31 characters, left-justified. This ensures that the right edges of your address card line up in the output. This is used in this example for cosmetic reasons.

With your AddressCard class in hand, you can write a test program to create an address card, set its values, and display it (see Program 15.8).

# Program 15.8 Test Program

```
#import "AddressCard.h"
#import <Foundation/NSAutoreleasePool.h>
int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc] init];
    NSString *aName = @"Julia Kochan";
    NSString *aEmail = @"jewls337@axlc.com";
    AddressCard *card1 = [[AddressCard alloc] init];

    [card1 setName:aName];
    [card1 setEmail:aEmail];

    [card1 release];
    [pool drain];
    return 0;
n
```

# Program 15.8 Output

```
========================================
Julia Kochan
jewls337@axlc.com

    o               o
========================================
```

In this program, the line [card1 release]; is used to release the memory that address card uses. You should realize from previous discussions that releasing an AddressCard object this way does not also release the memory you allocated for its name and email members. To make the AddressCard leak free,