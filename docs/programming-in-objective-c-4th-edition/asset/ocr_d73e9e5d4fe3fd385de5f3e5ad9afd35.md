```
#import "AddressCard.h"

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSString *aName = @"Julia Kochan";
        NSString *aEmail = @"jewls337@axlc.com";
        NSString *bName = @"Tony Iannanno";
        NSString *bEmail = @"tony.iannno@techfitness.com";

        AddressCard *card1 = [[AddressCard alloc]; init];
        AddressCard *card2 = [[AddressCard alloc]; init];

        [card1 setName:aName andEmail:aEmail];
        [card2 setName:bName andEmail:bEmail];

        [card1 print];
        [card2 print];
    }
    return 0;
}
```

# Program 15.9. Output

|==========================================|
| | |
| Julia Kochan |
| jewls337@axlc.com |
| | |
| |