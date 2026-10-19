Because of the specific nature of the code, it appears that the code is probably looping through the 12 months in a year. But are you sure? Would you bet your Monty Python collection on it?

In this case, you don’t need to use a named constant to support future flexibility: it’s not very likely that the number of months in a year will change anytime soon. But if the way the code is written leaves any shadow of a doubt about its purpose, clarify it with a well-named constant, like this:

```
Visual Basic Example of Clearer Code
For i = 1 To NUM_MONTHS_IN_YEAR
    profit(i) = revenue(i) - expense(i)
Next
```

This is better, but, to complete the example, the loop index should also be named something more informative:

```
Visual Basic Example of Even Clearer Code
For month = 1 To NUM_MONTHS_IN_YEAR
    profit(month) = revenue(month) - expense(month)
Next
```

This example seems quite good, but we can push it even one step further by using an enumerated type:

```
Visual Basic Example of Very Clear Code
For month = Month_January To Month_December
    profit(month) = revenue(month) - expense(month)
Next
```

With this final example, there can be no doubt about the purpose of the loop. Even if you think a literal is safe, use named constants instead. Be a fanatic about rooting out literals in your code. Use a text editor to search for 2, 3, 4, 5, 6, 7, 8, and 9 to make sure you haven’t used them accidentally.

Cross-Reference For details on simulating enumerated types, see "If Your Language Doesn’t Have Enumerated Types" in the previous section, Section 12.6.

Simulate named constants with appropriately scoped variables or classes If your language doesn’t support named constants, you can create your own. By using an approach similar to the approach suggested in the earlier Java example in which enumerated types were simulated, you can gain many of the advantages of named constants. Typical scoping rules apply: prefer local scope, class scope, and global scope in that order.

Use named constants consistently It’s dangerous to use a named constant in one place and a literal in another to represent the same entity. Some programming practices beg for errors; this one is like calling an 800 number and having errors delivered