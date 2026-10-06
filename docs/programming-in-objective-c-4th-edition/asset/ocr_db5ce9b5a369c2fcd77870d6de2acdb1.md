```
if (myCard != nil)
    [myCard print];
else
    NSLog("Not found!");
}
    return 0;
}
```

# Program 15.11. Output

Lookup: Stephen Kochan
====================================
| Stephen Kochan                     |
| steve@classroomM.com |
|                                    |
|             O              O |
====================================
Lookup: Haibo Zhang
Not found!

When the lookup method located Stephen Kochan in the address book (taking advantage of the fact that a non-case-sensitive match was made), the method returned the matching card immediately by executing the return statement, which terminates the loop and sends back the value of nextCard. That matching card was then given to the AddressCard's print method for display. In the case of the second lookup, the name Haibo Zhang was not found.