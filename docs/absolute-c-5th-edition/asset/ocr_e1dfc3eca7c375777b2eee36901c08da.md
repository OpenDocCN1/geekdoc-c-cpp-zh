# Rules on Overloading Operators

+   - When overloading an operator, at least one parameter (one operand) of the resulting overloaded operator must be of a class type.
- Most operators can be overloaded as a member of the class, a friend of the class, or a nonmember, nonfriend.
- The following operators can only be overloaded (nonstatic) members of the class: =, [], ~, and (().
- You cannot create a new operator. All you can do is overloading operators such as +, -, *, /, and so forth.
- You cannot change the number of arguments that an operator takes. For example, you cannot change * from a binary to a unary operator when you overload _; you cannot change ++ from a unary to a binary operator when you overload it.
- You cannot change the precedence of an operator. An overloaded operator has the same precedence as the ordinary version of the operator. For example, x*y + z always means x*y + z, unless x, y and z have been overloaded for the appropriate classes.
- The following operators cannot be overloaded: the dot operator (.), the scope resolution operator (::), sizeof ?, and the operator *, which is not discussed in this book.
- An overloaded operator cannot have default arguments.

# Self-Test Exercises

+   6. What is the difference between a friend function for a class and a member function for a class?

+   7. Complete the definition of the friend subtraction operator - in Display 8.3.

+   8. Suppose you wish to overload the operator = so that it applies to the type Money defined in Display 8.3. What do you need to add to the definition of Money given in Display 8.3?

# 8.3 References and More Overloaded Operators

Do not mistake the pointing finger for the moon.

> Zen saying

This section covers specialized, but important, overloading topics, including the assignment operator and the <<, [], ++, and -- operators. Because you need to understand returning a reference to correctly overload some of these operators, we also discuss this topic.