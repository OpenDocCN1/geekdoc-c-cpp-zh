if you want to make your own data types fit with the
standard library.

+   Logical operators
&&, ||, and ! combine truth values to form more
complex expressions.

+   Pointer operator and dereference operator
You use the unary operators & and * and the binary
operators -> and to address and to dereference. This
means that you retrieve an address, turn an address
data, or access a structure. You will see their use
in detail later.

+   Special operators
You can use ? and : together to write an either-or
expression. The comma , can be used as a sequence
operator in expressions. With C++20, the spaceship
operator <=> is added, which helps to implement the
relational operators.

+   Function-like operators
Strictly speaking, some special types also belong to
t operators that have real names and are used like
functions. These are type conversions such as
(int)value, sizeof(a), and some others. The fact that
are are operators means, for example, that you
cannot request the address from sizeof. You can only
give a function values and variables as parameters,
but with sizeof() you can also use a type, such as
sizeof(int). Strictly speaking, the brackets are also
optional; you could write sizeof a, for example, but
that would be very unusual.