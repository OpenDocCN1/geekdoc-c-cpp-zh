# Array Objects 349

```
[myBook addCard: card1];
[myBook addCard: card2];
[myBook addCard: card3];
[myBook addCard: card4];

// Look up a person by name

NSLog "@Lookup: Stephen Kochan";
myCard = [myBook lookup: "@Stephen Kochan"];

if (myCard != nil)
    [myCard print];
else
    NSLog "@Not found!");

// Now remove the entry from the phone book

[myBook removeCard: myCard];
[myBook list]; // verify it's gone

[card1 release];
[card2 release];
[card3 release];
[card4 release];
[myBook release];
[pool drain];

return 0;
```

# Program 15.12 Output

Lookup: Stephen Kochan

```
============================

Stephen Kochan
steve@classroom.com

          O           O

============================

======== Contents of: Linda's Address Book ========
Julia Kochan      jewls37@axlc.com
Tony Iannino      toniannino@techfitness.com
Jamie Baker       jbaker@classroom.com
==============================
```

After looking up Stephen Kochan in the address book and verifying that he's there, you pass the resulting AddressCard to your new removeCard: method to be removed. The resulting listing of the address book verifies the removal.