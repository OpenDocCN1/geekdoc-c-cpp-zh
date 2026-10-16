# NOTE

Ignore the code that references NSAutoreleasePool here. You learn about that in a future chapter.

Another unusual pointer situation that you will run into in this book centers around the use of pointers to objects, such as in the case of using an NSError object to get an error message back from a failed call. When I discuss this in Chapter 10, I cover this in more detail.

# Using operators

Like mathematics, programming languages typically support operators. An operator is a function that “operates” on variables and values. For example, the expression “5 + 4” contains the values 5 and 4 and the operator +. In this case, the + operator is said to be a binary operator. Therefore, it operates on two values, one on the left and one on the right, the 5 and the 4. Another type of operator is the unary operator. A unary operator only has one value that it operates upon. For example, the address-of operator, &, is a unary operator. It gets the address of the value that it operates on.

Table 2.2 shows most of the typical operators in Objective-C.

| Operator | Purpose |
|---|---|
| Table 2.2 Typical operators | |
| () [] -> . | Parentheses, array operations, dereference |
| ! ~ - + * & ++ -- | Not, add/subtraction (unary), dereference (unary), address-of (unary), increment (unary), decrement (unary) |
| * / % | Multiplication, Division, Modulus (binary) |
| << >> | Bitwise Shift (binary) |
| < <= > >= | Comparison Operators (binary) |
| == != | Comparison Operators (binary) |
| & | Bitwise AND (binary) |
| ^ | Bitwise XOR (binary) |
| | | Bitwise OR (binary) |
| && | AND (binary) |
| || | OR (binary) |
| = += -= *= /= %= &= |= ^= <<= >>= | Assignment Operators (binary) |