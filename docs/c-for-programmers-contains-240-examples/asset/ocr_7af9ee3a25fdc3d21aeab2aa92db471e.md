Function main (Fig. 11.14) creates three Date objects (lines 11–13)—d1 is initialized by default to January 1, 1900; d2 is initialized to December 27, 1992; and d3 is initialized to an invalid date. The Date constructor (defined in Fig. 11.13, lines 11–14) calls setDate to validate the month, day and year specified. An invalid month is set to 1, an invalid year is set to 1900 and an invalid day is set to 1.

Lines 15–16 of main output each of the constructed Date objects, using the overloaded stream insertion operator (defined in Fig. 11.13, lines 96–103). Line 16 of main uses the overloaded operator += to add seven days to d2. Line 18 uses function setDate to set d3 to February 28, 1992, which is a leap year. Then, line 20 preincrements d3 to show that the date increments properly to February 29. Next, line 22 creates a Date object, d4, which is initialized with the date July 13, 2002. Then line 26 increments d4 by 1 with the overloaded prefix increment operator. Lines 24–27 output d4 before and after the preincrement operation to confirm that it worked correctly. Finally, line 31 increments d4 with the overloaded postfix increment operator. Lines 29–32 output d4 before and after the postincrement operation to confirm that it worked correctly.

Overloading the prefix increment operator is straightforward. The prefix increment operator (defined in Fig. 11.13, lines 30–34) calls utility function helpIncrement (defined in Fig. 11.13, lines 76–93) to increment the date. This function deals with “wraparounds” or “carries” that occur when we increment the last day of the month. These carries require incrementing the month. If the month is already 12, then the year must also be incremented and the month must be set to 1. Function helpIncrement uses function endOfMonth to increment the day correctly.

The overloaded prefix increment operator returns a reference to the current Date object (i.e., the one that was just incremented). This occurs because the current object, *this, is returned as a Date &. This enables a preincremented Date object to be used as an lvalue, which is how the built-in prefix increment operator works for fundamental types.

Overloading the postfix increment operator (defined in Fig. 11.13, lines 38–45) is trickier. To emulate the effect of the postincrement, we must return an unincremented copy of the Date object. For example, if int variable x has the value 7, the statement

```
cout << x++ << endl;
```

outputs the original value of variable x. So we’d like our postfix increment operator to operate the same way on a Date object. On entry to operator++, we save the current object (*this) in temp (line 40). Next, we call helpIncrement to increment the current Date object. Then, line 44 returns the unincremented copy of the object previously stored in temp. Note that this function cannot return a reference to the local Date object temp, because a local variable is destroyed when the function in which it is declared exits. Thus, declaring the return type to this function as Date & would return a reference to an object that no longer exists. Returning a reference (or a pointer) to a local variable is a common error for which most compilers will issue a warning.

# 11.13 Standard Library Class string

In this chapter, you learned that you can build a String class (Figs. 11.9–11.11) that is better than the C-style, char * strings that C++ absorbed from C. You also learned that you can build an Array class (Figs. 11.6–11.8) that is better than the C-style, pointer-based arrays that C++ absorbed from C.