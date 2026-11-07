```
```cpp
change = change % HALF_DOLLAR;                 //Step 5

cout << "The number of quarters to be returned is "
     << change / QUARTER << endl;              //Step 6

change = change % QUARTER;                     //Step 7

cout << "The number of dimes to be returned is "
     << change / DIME << endl;                 //Step 8

change = change % DIME;                        //Step 9

cout << "The number of nickels to be returned is "
     << change / NICKEL << endl;               //Step 10

change = change % NICKEL;                      //Step 11

cout << "The number of pennies to be returned is "
     << change << endl;                        //Step 12

return 0;
```
```

**Sample Run:** In this sample run, the user input is shaded.

```
```text
Enter change in cents: 583

The change you entered is 583
The number of half-dollars to be returned is 11
The number of quarters to be returned is 1
The number of dimes to be returned is 0
The number of nickels to be returned is 1
The number of pennies to be returned is 3
```
```

# QUICK REVIEW

+   1. A C++ program is a collection of functions.
+   2. Every C++ program has a function called main.
+   3. A single-line comment starts with the pair of symbols `//` anywhere in the line.
+   4. Multiline comments are enclosed between `/*` and `*/`.
+   5. The compiler ignores comments.
+   6. Reserved words cannot be used as identifiers in a program.
+   7. All reserved words in C++ consist of lowercase letters (see Appendix A).