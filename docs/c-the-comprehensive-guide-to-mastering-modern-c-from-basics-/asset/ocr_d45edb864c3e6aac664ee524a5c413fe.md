```
db = db2; // compiler prevents dangerous
assignment
}
```

**Listing 16.19** With the deleted functions, the compiler prevents incorrect usage of the class.

I also have marked the db_ data field with const. This alone would prevent the compiler from generating an operator=, making the program safe in this regard. Because I manually remove the copy constructor with delete anyway, it doesn't hurt to play it safe and treat the assignment operator the same way.