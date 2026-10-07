# Array Objects 339

# Program 15.9 Test Program

```
#import "AddressCard.h"

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc] init];

    NSString *aName = "Julia Kochan";
    NSString *aEmail = "@jewls337@axlc.com";
    NSString *bName = "@Tony Iannino";
    NSString *bEmail = "@Tony.Iannino@techfitness.com";

    AddressCard *card1 = [[AddressCard alloc] init];
    AddressCard *card2 = [[AddressCard alloc] init];

    card1 setName:aName email:aEmail;
    card2 setName:bName email:bEmail;
    card1 print;
    card2 print;
    [card1 release];
    [card2 release];
    [pool drain];
    return 0;
}
```

# Program 15.9 Output

```
=================
Julia Kochan
jewls337@axlc.com

    O       O
=================

Tony Iannino
tony.iannino@techfitness.com

    O       O
=================
```