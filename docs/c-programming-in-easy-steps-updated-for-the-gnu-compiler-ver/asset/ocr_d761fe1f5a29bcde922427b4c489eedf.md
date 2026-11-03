# ...cont'd

+   4. Now, insert statements requesting user input to be assigned to a variable.
+   
+   ```c
+   printf("Enter the diameter of a circle in millimeters: ");
+   scanf("%f", &diameter);
+   ```

+   5. Next, add statements to calculate values for the other three variables using the constant value and user input.
+   
+   ```c
+   circ = PI * diameter;
+   radius = diameter / 2;
+   area = PI * (radius * radius);
+   ```

![](bbox=[0.694, 0.126, 0.806, 0.221])

Here the * asterisk character is the arithmetical multiplication operator, and the / forward slash character is the division operator. Arithmetical operators are demonstrated fully in the next chapter.

+   6. Now, insert statements to output the calculated values formatted to two decimal places.
+   
+   ```c
+   printf("\n\tCircumference is %.2f mm", circ);
+   printf("\n\tAnd the area is %.2f sq.mm\n", area);
+   ```

+   7. At the end of the main function block, return a zero integer value, as required by the function declaration.
+   
+   ```c
+   return 0;
+   ```

+   8. Save the program file, then compile and execute the program, entering data when requested, to see the calculated output.

![](bbox=[0.117, 0.587, 0.649, 0.694])

![](bbox=[0.463, 0.676, 0.603, 0.808])

![](bbox=[0.117, 0.768, 0.649, 0.94])

![](bbox=[0.694, 0.57, 0.808, 0.662])

Remember that the & address of operator must precede the variable name in scanf() to assign input to the variable.