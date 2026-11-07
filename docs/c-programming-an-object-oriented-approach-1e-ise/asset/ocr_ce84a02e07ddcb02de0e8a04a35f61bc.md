# **Program 10.26** Testing four customized functions (Continued)

```
    29  cout << endl;
    30  // Testing popBack function
    31  cout << "String before calling popBack: " << strg << endl;
    32  char c2 = popBack (strg);
    33  cout << "String after calling popBack: " << strg << endl;
    34  cout << "The popped character: " << c2 << endl;
    35  cout << endl;
    36  return 0;
    37  }
```

Run:
String before calling pushFront: abcdefgh  
String after calling pushFront: Aabcdefgh  

String before calling pushBack: Aabcdefgh  
String after calling pushBack: AabcdefghZ  

String before calling popFront: AabcdefghZ  
String after calling popFront: abcdefghZ  
The popped character: A  

String before calling popBack: abcdefghZ  
String after calling popBack: abcdefgh  
The popped character: Z

# ### 10.3.2 Conversion in Positional Number Systems

In computer science we use different positional numbering systems; these are described in Appendix B: binary, octal, decimal, and hexadecimal. Each positional numbering system uses a set of symbols and a base. The *base* defines the total number of symbols used in the system. Table 10.3 shows the base and the symbols we work with in programming. Note that the values of symbols A, B, C, D, E, F are 10, 11, 12, 13, 14, and 15, respectively.

Although all of these number systems represent an integer using different notations, the decimal system is the only one that can be directly used as an integer in a program. A number in other systems must be represented as a string of characters.

# **Table 10.3** Positional numbering system

| System | Base | Symbols |
|---|---|---|
| binary | 2 | 0, 1 |
| octal | 8 | 0, 1, 2, 3, 4, 5, 6, 7 |
| decimal | 10 | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 |
| hexadecimal | 16 | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F |