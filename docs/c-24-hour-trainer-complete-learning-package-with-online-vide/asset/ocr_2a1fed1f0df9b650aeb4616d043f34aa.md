# EXERCISES

1. Providing methods that combine `ComplexNumbers` and `doubles` requires a lot of similar code. For example, to perform addition with ComplexNumbers, you need to overload the + operator three times to handle `ComplexNumber + ComplexNumber`, `ComplexNumber + double`, and `double + ComplexNumber`.

Fortunately, there's a better approach. Just provide an implicit conversion operator to convert a `double` into a `ComplexNumber`. Now if the program needs to perform the operation `ComplexNumber + double`, it automatically converts the `double` into a `ComplexNumber` and can then perform the addition.

Copy the program you built in this lesson's Try It and remove the code that combines `ComplexNumbers` with `doubles`. Then add an implicit conversion operator to convert `doubles` into `ComplexNumbers`. Verify that the program still works.

2. Copy the program you built for Exercise 1 and overload the `ComplexNumber` class's / operator to perform division using this equation:

$$\frac{a + bi}{c + di} = \frac{(ac + bd) + i(bc - ad)}{c^2 + d^2}$$

Use this operator to define operators for `ComplexNumber / double` and `double / ComplexNumber`. (Hint: Don't perform all of the calculations for these. Convert the `double` into a `ComplexNumber` and then use the previous definition of /.)

Change the main program to calculate A / B. Verify these calculations:

+   - `(10+11i) / (3+2i) = 4 + 1i`
+   - `(15+24i) / 3 = 5 + 8i`
+   - `4 / (1+1i) = 2 - 2i`

3. Build an application with an `OrderItem` class that has the properties `Description`, `Quantity`, and `PriceEach`. Also make an `Order` class that has the properties `CustomerName` and `Items`, which is a `List<OrderItem>`. Then overload the `Order` class's + operator so you can use it to add `OrderItems` to an `Order`. Build a simple user interface to test the classes.
Hints:

+   - Give the form a class-level `Order` object and then add items to it.
+   - Make the + operator return the `Order` to which it is adding an item.
+   - Override the `OrderItem` class's `ToString` method so you can easily display items in a `ListBox`.

4. [Advanced] By default, a class's `Equals` method tests reference equality. That means it considers two variables equal if they refer to the same instance of the class. For example, it would consider two `Employee` variables different if they refer to separate instances of the class even if they have the same `FirstName` and `LastName` property values. Sometimes that makes sense, but other times it's inconvenient.