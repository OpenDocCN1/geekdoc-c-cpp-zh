d) Vary the control variable from 20 to 2 in increments of −2.

```
for (int i = 20; i >= 2; i -= 2)
```

**Answer:** c) is incorrect. The for statement actually generates the sequence 2, 5, 8, 11, 14, 17. It does not generate the value 15 in the original series.

# 4.6 **Switch Multiple-Selection Statement**

In Chapter 3, we discussed the if single-selection and the if...else double-selection statements. Occasionally, an algorithm will contain a series of decisions that test a variable or expression separately for each of the integer values it may assume, then perform different actions. This is called multiple selection. C provides the switch multiple-selection statement to handle such decision making.

The switch statement consists of a series of case labels, an optional default case and statements to execute for each case. Figure 4.5 uses switch to count the number of each different letter grade students earned on an exam.

```
```c
// fig04_05.c
// Counting letter grades with switch.
#include <stdio.h>

int main(void) {
   int aCount = 0;
   int bCount = 0;
   int cCount = 0;
   int dCount = 0;
   int fCount = 0;

   puts("Enter the letter grades.");
   puts("Enter the EOF character to end input.");
   int grade = 0; // one grade

   // loop until user types end-of-file key sequence
   while ((grade = getchar()) != EOF) {

      // determine which grade was input
      switch (grade) { // switch nested in while
         case 'A': // grade was uppercase A
         case 'a': // or lowercase a
            ++aCount;
            break; // necessary to exit switch
         case 'B': // grade was uppercase B
         case 'b': // or lowercase b
            ++bCount;
            break;
         case 'C': // grade was uppercase C
         case 'c': // or lowercase c
            ++cCount;
            break;
```
```

**Fig. 4.5** | Counting letter grades with `switch`. (Part 1 of 2.)