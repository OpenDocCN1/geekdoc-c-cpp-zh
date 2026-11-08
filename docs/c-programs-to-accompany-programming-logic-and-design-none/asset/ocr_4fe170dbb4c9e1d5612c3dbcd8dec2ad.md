```
b. int val1 = 10, val2 = 20;
void printSum(int num1, int num2)
```

```
c. double salary = 37500, percent = .10;
void increase(double sal, double pcnt)
```

# ## LAB 7-3: WRITING FUNCTIONS THAT REQUIRE MULTIPLE PARAMETERS

In this lab, you complete a partially written C++ program that includes a function requiring multiple parameters (arguments). The program prompts the user for an item price and the number of items ordered. If the item's price is less than $5.00, the program should apply a 5% discount; if the item's price is between $5.00 and $9.99, the program should apply a 10% discount; if the item is $10.00 or more, the program should apply a 15% discount. Once the discount is applied, the program should calculate the total price for the number of items purchased and then display the original price, the discount percent, the discounted price, the quantity ordered, and the total price for the items ordered. The source code file provided for this lab includes the variable declarations and the input statements. Comments are included in the file to help you write the remainder of the program.

+   1. Open the source code file named `DiscountPrices.cpp` using Notepad or the text editor of your choice.
+   2. Write the C++ statements as indicated by the comments.
+   3. Save this source code file in a directory of your choice and then make that directory your working directory.
+   4. Compile the source code file `DiscountPrices.cpp`.
+   5. Execute the program.

# ## WRITING FUNCTIONS THAT RETURN A VALUE

Thus far in this book, none of the functions you have written (except for the `main` function) return a value. The header for each of these functions includes the keyword `void`, as in

```
void nameAndAddress()
```

indicating that the function does not return a value. However, as a programmer, you will often find that you need to write functions that do return a value. In C++, a function can only return

![](bbox=[0.95, 0.482, 1.0, 0.529])