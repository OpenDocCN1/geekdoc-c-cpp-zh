# 6.2 RESTRICTIONS UNDER OPERATOR OVERLOADING

Though operator overloading is possible, it has its own set of restrictions, which are listed as follows:

Operator overloading provides additional meaning to an operator.

+   1. Operators do not lose their original meaning; instead, they have an additional meaning when overloaded. One cannot change the original meaning of an operator.
+   2. New operators cannot be devised. Only existing operators with given restrictions can be overloaded.
+   3. Operators will have an additional meaning, but will not have an additional precedence. The precedence remains the same.
+   4. Operators cannot change the number of arguments that were available in the original form. Hence, ‘+’ in the binary form can only have two arguments. It cannot be overloaded with three arguments.
+   5. Operators can only be overloaded for user-defined types. All overloaded operators must have at least one argument as a user-defined type.
+   6. Except (), no other operator can have a default argument.
+   7. Some operators can never be overloaded.

# 6.2.1 Operators that Cannot be Overloaded

The following operators cannot be overloaded:

+   1. Dot operator for member access (.)
+   2. Dereference member to class operator (.*)
+   3. Scope resolution operator (::)
+   4. Size of operator (sizeof)
+   5. Conditional ternary operator (?:)
+   6. Casting operators (static_cast<>, dynamic_cast<>, reinterpret_cast<>, and const_cast<>)
+   7. # and ## tokens for macro preprocessors

> Note One may ask why these operators cannot be overloaded. Consider overloading the dot operator. If it is overloaded, a class member operation gets a new meaning, which may lead to serious errors. A compiler developer must deal with the possible complexities that arise out of such errors and help the programmer by providing probable reasons for the error. If C++ allows such code, it can easily confuse the compiler with unforeseen side effects. It is for the same reason that C++ does not allow adding new operators. C++ also does not allow the global definition of certain operators (e.g., = operator). Many languages, including Java, do not provide operator overloading as it is a very difficult problem to manage.

# 6.2.2 Operators that Cannot be Overloaded as Friends

As pointed out earlier, operators are overloaded as functions. For a function to operate on a class, it should be either a member or a friend. The consequence is that the operators can be overloaded in two distinct ways, that is, as members or as friends. The following operators cannot be overloaded as friends:

+   1. Assignment operator =
+   2. Function call operator ()
+   3. Array subscript operator []
+   4. Access to class member using pointer to object operator ->