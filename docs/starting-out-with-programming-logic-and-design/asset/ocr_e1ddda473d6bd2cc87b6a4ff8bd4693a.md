# Chapter 6 Functions

Because functions return a value, they can be useful in specific situations. For example, you can use a function to prompt the user for input, and then it can return the value entered by the user. Suppose you've been asked to design a program that calculates the sale price of an item in a retail business. To do that, the program would need to get the item's regular price from the user. Here is a function you could define for that:

```
Function Real getRegularPrice()
// Local variable to hold the price.
Declare Real price

// Get the regular price.
Display "Enter the item's regular price.
Input price

// Return the regular price.
Return price
End Function
```

Then, elsewhere in the program, you could call that function, as shown here:

```
Set regularPrice = getRegularPrice()
```

When this statement executes, the getRegularPrice function is called, which gets a value from the user and returns it. It then assigns to the regularPrice variable.

You can also use functions to simplify complex mathematical expressions. For example, calculating the sale price of an item like it would be a simple task: you calculate the discount and subtract it from the regular price. In a program, a statement that performs this calculation is not as straightforward, as shown in the following example (Assume DISCOUNT_PERCENTAGE is a global constant that is defined in the program, and it specifies the percentage of the discount).

```
Set salePrice = regularPrice - (regularPrice * DISCOUNT_PERCENTAGE)
```

This statement isn't easy to understand because it performs so many steps: it calculates the discount amount, subtracts that from regularPrice, and assigns the result to salePrice. You could simplify the statement by breaking out part of the math expression and placing it in a function. Here is a function named discount that accepts an item's price as an argument and returns the discount of the:

```
Function Real discount(Real price)
Return price * DISCOUNT_PERCENTAGE
End Function
```

You could call the function in your calculation:

```
Set salePrice = regularPrice - discount(regularPrice)
```

This statement is easier to read than the one previously, and it is clearer that the discount is being subtracted from the regular price. The pseudocode in Program 6-7 shows the complete sale price calculating using the functions just described.