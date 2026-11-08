# ## LAB 5-2: USING A SENTINEL VALUE TO CONTROL A WHILE LOOP

In this lab, you write a `while` loop that uses a sentinel value to control a loop in a C++ program provided with the data files for this book. You also write the statements that make up the body of the loop. The source code file already contains the necessary variable declarations and output statements. When completed, the program should print a payoff schedule for a credit card company customer. At the beginning of every month, 1.3% interest is added to the balance, and then the customer makes a payment equal to 4% of the current balance. When the balance reaches $15.00 or less, the customer can pay off the account. As you will see, this program generates a lot of output, even for one customer.

+   1. Open the source code file named `Payoff.cpp` using Notepad or the text editor of your choice.
+   
+   2. Write the `while` loop using a sentinel value to control the loop and also write the statements that make up the body of the loop. The output statements within the loop have already been written for you.
+   
+   3. Save this source code file in a directory of your choice and then make that directory your working directory.
+   
+   4. Compile the source code file `Payoff.cpp`.
+   
+   5. Execute the program. Input the following:
+   
+       Account Number: 6789A
+   
+       Customer Name: Jeanne Johnson
+   
+       Balance: 120.00
+   
+   6. Record the final balance amount when the loan may be paid off.

# ## WRITING A FOR LOOP IN C++

In Chapter 5 of *Programming Logic and Design, Fifth Edition*, you learned that a `for` loop is a **definite** loop; this means this type of loop will execute a definite number of times. The following is the syntax for a `for` loop in C++:

```
```cpp
for (expression1; expression2; expression3)
    statement;
```
```