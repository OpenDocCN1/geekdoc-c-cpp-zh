```
// Add some cards to the address book

[myBook addCard: card1];
[myBook addCard: card2];
[myBook addCard: card3];
[myBook addCard: card4];
```

```
// Look up a person by name

NSLog("@Lookup: Stephen Kochan");
    myCard = [myBook lookup: @"Stephen Kochan"];

    if (myCard != nil)
        [myCard print];
    else
        NSLog("@Not found!");");"
```

```
// Now remove the entry from the phone book

[myBook removeCard: myCard];
[myBook list]; // verify it's gone
}

return 0;
}
```

# Program 15.12. Output

Lookup: Stephen Kochan
===========================================
| |
| Stephen Kochan | |