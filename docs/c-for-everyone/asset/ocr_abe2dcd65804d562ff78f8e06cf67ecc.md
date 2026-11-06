# Table 7 Formatting Output

| Output Statement | Output | Comment |
|---|---|---|
| `cout << 12.345678;` | `12.3457` | By default, a number is printed with 6 significant digits. |
| `cout << fixed`<br>`    << setprecision(2)`<br>`    << 12.30;` | `12.30` | Use the fixed and setprecision manipulators to control the number of digits after the decimal point. |
| `cout << ":" << setw(6)`<br>`    << 12;` | `:    12` | Four spaces are printed before the number, for a total width of 6 characters. |
| `cout << ":" << setw(2)`<br>`    << 123;` | `:123` | If the width not sufficient, it is ignored. |
| `cout << setw(6)`<br>`    << ":" << 12;` | `     :12` | The width only refers to the next item. Here, the `:` is preceded by five spaces. |

![](bbox=[0.146, 0.431, 0.226, 0.516])

# SELF CHECK

+   15. What is wrong with the following statement sequence?
+   
+   ```cpp
+   cout << "Please enter the unit price: ";
+   double unit_price;
+   cin >> unit_price;
+   int quantity;
+   cin >> quantity;
+   ```

+   16. What is problematic about the following statement sequence?
+   
+   ```cpp
+   cout << "Please enter the unit price: ";
+   int unit_price;
+   cin >> unit_price;
+   ```

+   17. What is the output of the following statement sequence?
+   
+   ```cpp
+   double bottles = 10;
+   cout << "The total volume is" << 2 * bottles;
+   ```

+   18. How do you print the floating-point variable `total_price` in dollars and cents, like this: `$1.22`?

+   19. Using the `setw` manipulator, improve the output statement
+   
+   ```cpp
+   cout << "Bottles: " << bottles << endl
+        << "Cans: " << cans << endl;
+   ```
+   
+   so that the output looks like this:
+   
+   ```text
+   Bottles:        8
+   Cans:          24
+   ```
+   
+   The numbers to the right should line up. (You may assume that the numbers have at most 8 digits.)

**Practice It**  Now you can try these exercises at the end of the chapter: R2.7, R2.8, P2.6, P2.7.