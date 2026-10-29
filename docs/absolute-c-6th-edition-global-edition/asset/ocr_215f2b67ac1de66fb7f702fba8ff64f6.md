of handshakes that would be made in a room of two people, or a total of three handshakes.

If a fourth person enters the room, he or she must shake hands with each of the three people already there. This is three handshakes in addition to the number of handshakes that would be made in a room of three people, or six handshakes.

If you can generalize this to n handshakes, you should be able to write the recursive solution.

# 10. Consider a frame of bowling pins, where each * represents a pin:

*
  * *
* * *
* * * *
* * * * * *

There are five rows and a total of fifteen pins. If we had only the top four rows, there would be a total of ten pins. If we had only the top three rows, there would be a total of six pins. If we had only the top two rows, there would be a total of three pins. If we had only the top row, there would be a total of one pin.

Write a recursive function that takes as input the number of rows, n, and outputs the total number of pins that would exist in a pyramid with n rows. Your program should allow for values of n that are larger than 5.

# 11. Write a recursive function named contains with the following header:

```
bool contains (char *haystack, char *needle)
```

The function should return true if the C-string needle is contained within the C-string haystack and false if needle is not in haystack. For example,

```
contains("C++ programming", "ogra") should return true
contains("C++ programming", "grammy") should return false
```

You are not allowed to use the string class substr or find functions to determine a match.

# 12. The following diagram is an example of a deterministic finite state automaton, or DFA. This particular DFA describes an algorithm to determine if a sequence of characters is a properly formatted monetary amount with commas. For example, "$1,000" and "$25" and "$551,323,991,391" are properly formatted but "1,000" (no initial $) and "$1000" (missing comma) and "$5424,132" (missing comma) are not.