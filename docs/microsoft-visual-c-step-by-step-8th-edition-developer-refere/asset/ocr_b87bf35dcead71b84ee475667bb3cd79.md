when defining your own types. With C#, you can also overload many of the existing operator symbols for your own types, although the syntax is slightly different. When you do this, the operators you implement automatically fall into a well-defined framework with the following rules:

+   - You cannot change the precedence and associativity of an operator. Precedence and associativity are based on the operator symbol (for example, +) and not on the type (for example, int) on which the operator symbol is being used. Hence, the expression a + b * c is always the same as a + (b * c) regardless of the types of a, b, and c.
+   - You cannot change the multiplicity (the number of operands) of an operator. For example, * (the symbol for multiplication) is a binary operator. If you declare a * operator for your own type, it must be a binary operator.
+   - You cannot invent new operator symbols. For example, you can’t create an operator symbol such as ** for raising one number to the power of another number. You’d have to define a method to do that.
+   - You can’t change the meaning of operators when they are applied to built-in types. For example, the expression 1 + 2 has a predefined meaning, and you’re not allowed to override this meaning. If you could do this, things would be too complicated.
+   - There are some operator symbols that you can’t overload. For example, you can’t overload the dot (.) operator, which indicates access to a class member. Again, if you could do this, it would lead to unnecessary complexity.

# Tip

You can use indexers to simulate [] as an operator. Similarly, you can use properties to simulate assignment (=) as an operator, and you can use delegates to mimic a function call as an operator.

# Overloaded operators

To define your own operator behavior, you must overload a selected operator. You use method-like syntax with a return type and parameters, but the name of the method is the keyword operator together with the operator symbol you are declaring. For example, the following code shows a user-defined structure named Hour that defines a binary + operator to add together two instances of Hour:

Click here to view code image

```
struct Hour
{
    public Hour(int initialValue)
```