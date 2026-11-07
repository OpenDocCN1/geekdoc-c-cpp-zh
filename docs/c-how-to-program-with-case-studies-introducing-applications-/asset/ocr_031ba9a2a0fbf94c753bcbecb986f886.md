**3.27** *(Validating User Input)* Modify the program in Figure 3.6 to validate its inputs. For each input, if the value is other than 1 or 2, keep looping until the user enters a correct value.

**3.28** What does the following program print?

```
```c
#include <stdio.h>

int main(void) {
   int count = 1; // initialize count

   while (count <= 10) { // loop 10 times
      // output 1 line of text
      puts(count % 2 ? "*****" : "+++++++");
      ++count; // increment count
   } // end while
} // end function main
```
```

**3.29** What does the following program print?

```
```c
#include <stdio.h>

int main(void) {
   int row = 10; // initialize row

   while (row >= 1) { // loop until row < 1
      int column = 1; // set column to 1 as iteration begins

      while (column <= 10) { // loop 10 times
         printf("%s", (row % 2) ? ">" : "<"); // output
         ++column; // increment column
      } // end inner while

      --row; // decrement row
      puts(""); // begin new output line
   } // end outer while
} // end function main
```
```

**3.30** *(Dangling-Else Problem)* Determine the output for each of the following when x is 9 and y is 11, and when x is 11 and y is 9. The compiler ignores the indentation in a C program. Also, the compiler always associates an else with the previous if unless told to do otherwise by the placement of braces { }. For instance, you may not be sure which if an else matches, so this is referred to as the “dangling-else” problem. We eliminated the indentation from the following code to make the problem more challenging. *[Hint: Apply the indentation conventions you have learned.]*

```
```c
a) if (x < 10)
      if (y > 10)
         puts("*****");
      else
         puts("#####");
      puts("$$$$$");
```
```