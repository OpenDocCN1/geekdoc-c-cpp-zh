After a variable has been declared in a program, typically a programmer uses it to refer to the variable’s contents (its value). The value’s memory location is generally of little concern to programmers. The compiler, however, must know where each value is stored and locate each variable correctly. For this task, the compiler uses the variable name to locate the first byte of storage previously allocated to the variable. Knowing the variable’s data type then allows the compiler to store or retrieve the correct number of bytes.

# EXERCISES 2.3

+   1. **(Practice)** State whether the following variable names are valid. If they’re invalid, state the reason.
+   
+   ```text
+   prod_a      c1234       abcd        __c3       12345
+   newbal      while       $total      new bal     a1b2c3d4
+   9ab6        sum.of      average     grade1      finGrade
+   ```

+   2. **(Practice)** State whether the following variable names are valid. If they’re invalid, state the reason. Also, indicate which of the valid variable names shouldn’t be used because they convey no information about the variable.
+   
+   ```text
+   salestax    a243        r2d2        firstNum     cc_a1
+   harry       sue         c3p0        average      sum
+   maximum     okay        a           awesome      goforit
+   3sum        for         tot.a1      c$five      netpay
+   ```

+   3. **(Practice)**
+      a. Write a declaration statement to declare that the variable `count` will be used to store an integer.
+      b. Write a declaration statement to declare that the variable `grade` will be used to store a floating-point number.
+      c. Write a declaration statement to declare that the variable `yield` will be used to store a double-precision number.
+      d. Write a declaration statement to declare that the variable `initial` will be used to store a character.

+   4. **(Practice)** Write a single declaration statement for each set of variables:
+      a. `num1`, `num2`, and `num3` used to store integer numbers
+      b. `grade1`, `grade2`, `grade3`, and `grade4` used to store double-precision numbers
+      c. `temp1`, `temp2`, and `temp3` used to store double-precision numbers
+      d. `let1`, `let2`, `let3`, and `let4` used to store characters

+   5. **(Practice)** Write a single declaration statement for each set of variables:
+      a. `firstnum` and `secnum` used to store integers
+      b. `price`, `yield`, and `coupon` used to store double-precision numbers
+      c. `average` used to store a double-precision number