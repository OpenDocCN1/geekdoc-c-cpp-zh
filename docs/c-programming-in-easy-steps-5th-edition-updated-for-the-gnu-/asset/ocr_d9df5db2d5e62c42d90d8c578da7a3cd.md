operator is useful in C programming to toggle the value of a variable in successive loop iterations with a statement like var = !var. This ensures that on each pass the value is reversed, like flicking a light switch on and off.

![](bbox=[0.1, 0.25, 0.28, 0.45])

The term "Boolean" refers to a system of logical thought developed by the English mathematician George Boole (1815-1864).

In C programming, a zero represents the Boolean false value; and any non-zero value, such as 1, represents the Boolean true value.

+   1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
+   ```c
+   #include <stdio.h>
+   ```
+   2. Add a main function that declares and initializes two integer variables
+   ```c
+   int main()
+   {
+     int yes = 1, no = 0;
+   }
+   ```
+   3. Next, in the main function block, output the result of logic operations performed on the variables
+   ```c
+   printf(" AND (no&&no): %d \n", no && no );
+   printf(" AND (yes&&no): %d \n", yes && no );
+   printf(" AND (yes&&yes): %d \n", yes && yes );
+   printf(" OR (no||no): %d \n", no || no );
+   printf(" OR (yes||no): %d \n", yes || no );
+   ```

![](bbox=[0.1, 0.62, 0.25, 0.78])

logic.c