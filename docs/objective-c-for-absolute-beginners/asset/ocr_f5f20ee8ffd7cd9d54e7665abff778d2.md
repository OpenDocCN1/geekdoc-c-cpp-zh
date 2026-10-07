break; // This indicates that this is the end of the "case 'a':"
case 'b':

break;
case 'c': // If there is a case without a break, the program continues to execute.
case 'd': // So, in this case, if value is a 'c' or a 'd', this code will
executed.

break;
default: // Default is optional and is only used if there is no case
statement
the switch // for 'value'. So, if value was equal to 'x', the default part of
break // statement will be executed since there is no "case 'x':" present.

) // End of the switch statement.
The switch statement is very powerful, and it simplifies and streamlines comparisons of
an ordinal type to several possible constants. That said, this is also the limiting factor of
t switch statement. It is not possible, for example, to use the switch statement to
compare NSString to a series of string constants. This is because an
NSString value is not an ordinal type. The switch statement also must compare
ordinal type to a constant. Therefore, it is not possible to write:

```
switch (value) {
case variable: //case must be a constant, not a variable.
```

break;
While it does seem that these are severe limitations to the switch statement, the switch
statement is still a very powerful statement that can be used to simplify if/else
statements.

# Summary

We've reached the end of the chapter! Here is a summary of the things that were
covered.

+   - Comparisons
  - Comparing data is an integral part of any application.
- Relational operators
  - You learned about the six standard relational operators and how
each is used.
- Integers
  - Integers are the easiest pieces of information to compare. They
    learned how comparison of integers will be used in your
    programs and how to implement it.