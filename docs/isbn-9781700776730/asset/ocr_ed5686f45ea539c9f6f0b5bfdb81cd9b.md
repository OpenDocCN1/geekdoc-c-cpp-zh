+   - equality ==, !=
- assignment =, +=, -=, *=, /=, &=, |=, =, ^, <=, >==
- comma ,
- increment and decrement ++, --
- subscript []
- function call ()
- class pointer ->
- member pointer selector ->*\n- free store allocator new
- recycling delete

You cannot overload these operators:

+   - member .
- member object selector .*
- ternary conditional ?:
- sizeof sizeof
- scope resolution ::

Note the following:

+   - You can only overload existing operators. That is, you cannot design new operators, tempting as it may be:

```
=, <>, |x|, **
```

Focus on Object-Oriented Programming with C++ Page 234