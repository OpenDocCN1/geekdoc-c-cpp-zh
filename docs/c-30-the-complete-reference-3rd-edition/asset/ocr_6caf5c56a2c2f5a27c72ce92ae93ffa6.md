if you remove the cast, the program will not compile.

There are a few restrictions to conversion operators:

+   - Either the target type or the source type of the conversion must be the class in which the conversion is declared. You cannot, for example, redefine the conversion from double to int.
+   - You cannot define a conversion to or from object.
+   - You cannot define both an implicit and an explicit conversion for the same source and target types.
+   - You cannot define a conversion from a base class to a derived class. (See Chapter 11 for a discussion of base and derived classes.)
+   - You cannot define a conversion from or to an interface. (See Chapter 12 for a discussion of interfaces.)

In addition to these rules, there are suggestions that you should normally follow when choosing between implicit and explicit conversion operators. Although convenient, implicit conversions should be used only in situations in which the conversion is inherently error-free. To ensure this, implicit conversions should be created only when these two conditions are met: First, that no loss of information, such as truncation, overflow, or loss of sign, occurs. Second, that the conversion does not cause an exception. If the conversion cannot meet these two requirements, then you should use an explicit conversion.

# Operator Overloading Tips and Restrictions

The action of an overloaded operator as applied to the class for which it is defined need not bear any relationship to that operator's default usage, as applied to C#'s built-in types. However, for the purposes of the structure and readability of your code, an overloaded operator should reflect, when possible, the spirit of the operator's original use. For example, the + relative to ThreeD is conceptually similar to the + relative to integer types. There would be little benefit in defining the + operator relative to some class in such a way that it acts more the way you would expect the / operator to perform, for instance. The central concept is that while you can give an overloaded operator any meaning you like, for clarity it is best when its new meaning is related to its original meaning.

There are some restrictions to overloading operators. You cannot alter the precedence of any operator. You cannot alter the number of operands required by the operator, although your operator method could choose to ignore an operand. There are several operators that you cannot overload. Perhaps most significantly, you cannot overload any assignment operator, including the compound assignments, such as +=. Here are the other operators that cannot be overloaded. (This list includes several operators that are discussed later in this book.)

| && | () | . | ? |
|---|---|---|---|
| ?? | [ ] | || | = |
| => | -> | as | checked |
| default | is | new | sizeof |
| typeof | unchecked |  |  |