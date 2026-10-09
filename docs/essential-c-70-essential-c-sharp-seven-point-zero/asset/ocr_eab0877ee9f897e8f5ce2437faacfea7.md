In contrast, consider what would happen if you provided a – operator that had two Coordinates as parameters and returned a double corresponding to the distance between the two coordinates. Adding a double to a Coordinate is undefined, so you could not string together operators and operands. Caution is in order when defining operators that return a different type, because doing so is counterintuitive.

# Combining Assignment with Binary Operators (+=, -=, *=, /=, %=, &=, ...)

As previously mentioned, there is no support for overloading the assignment operator. However, assignment operators in combination with binary operators (+=, -=, *=, /=, %=, &=, |=, ^=, <<=, and >>=) are effectively overloaded when overloading the binary operator. Given the definition of a binary operator without the assignment, C# automatically allows for assignment in combination with the operator. Using the definition of Coordinate in Listing 10.7, therefore, you can have code such as

```
coordinate += arc;
```

which is equivalent to the following:

```
coordinate = coordinate + arc;
```

# Conditional Logical Operators (&&, ||)

Like assignment operators, conditional logical operators cannot be overloaded explicitly. However, because the logical operators & and | can be overloaded, and the conditional operators comprise the logical operators, effectively it is possible to overload conditional operators. x && y is processed as x & y, where y must evaluate to true. Similarly, x || y is processed as x | y only if x is false. To enable support for evaluating a type to true or false—in an if statement, for example—it is necessary to override the true/false unary operators.

# Unary Operators (+, -, !, ~, ++, --, true, false)

Overloading unary operators is very similar to overloading binary operators, except that they take only one parameter, also of the containing type. Listing 10.9 overloads the + and - operators for Longitude and Latitude and then uses these operators when overloading the same operators in Arc.