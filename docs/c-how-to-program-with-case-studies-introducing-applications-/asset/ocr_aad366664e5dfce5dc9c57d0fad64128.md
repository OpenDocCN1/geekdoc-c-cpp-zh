d) Error: Improper relational operator used in the while iteration-continuation condition.

Correction: Use `<=` rather than `<`.

# Exercises

**4.5** Find the error in each of the following. *(Note: There may be more than one error.)*

+   a) ```c
+   For (x = 100, x >= 1, ++x) {
+       printf("%d\n", x);
+   }
+   ```

+   b) The following code should print whether a given integer is odd or even:
+   
+   ```c
+   switch (value % 2) {
+       case 0:
+           puts("Even integer");
+       case 1:
+           puts("Odd integer");
+   }
+   ```

+   c) The following code should input an integer and a character and print them. Assume the user types as input 100 A.
+   
+   ```c
+   scanf("%d", &intVal);
+   charVal = getchar();
+   printf("Integer: %d\nCharacter: %c\n", intVal, charVal);
+   ```

+   d) ```c
+   for (x = .000001; x == .0001; x += .000001) {
+       printf("%.7f\n", x);
+   }
+   ```

+   e) The following code should output the odd integers from 999 to 1:
+   
+   ```c
+   for (x = 999; x >= 1; x += 2) {
+       printf("%d\n", x);
+   }
+   ```

+   f) The following code should output the even integers from 2 to 100:
+   
+   ```c
+   counter = 2;
+   Do {
+       if (counter % 2 == 0) {
+           printf("%d\n", counter);
+       }
+       counter += 2;
+   } While (counter < 100);
+   ```

+   g) The following code should sum the integers from 100 to 150 (assume total is initialized to 0):
+   
+   ```c
+   for (x = 100; x <= 150; ++x) {
+       total += x;
+   }
+   ```