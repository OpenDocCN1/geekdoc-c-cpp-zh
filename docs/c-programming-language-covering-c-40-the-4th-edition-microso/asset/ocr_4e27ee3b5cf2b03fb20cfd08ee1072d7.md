The term “evaluated only once” means that in the evaluation of x op y, the results of any constituent expressions of x are temporarily saved and then reused when performing the assignment to x. For example, in the assignment A()[B()] += C(), where A is a method returning int[], and B and C are methods returning int, the methods are invoked only once, in the order A, B, C.

When the left operand of a compound assignment is a property access or an indexer access, the property or indexer must have both a get accessor and a set accessor. If this is not the case, a binding-time error occurs.

The second rule above permits x op= y to be evaluated as x = (T)(x op y) in certain contexts. The rule exists such that the predefined operators can be used as compound operators when the left operand is of type sbyte, byte, short, ushort, or char. Even when both arguments are of one of those types, the predefined operators produce a result of type int, as described in §7.3.6.2. Thus, without a cast, it would not be possible to assign the result to the left operand.

The intuitive effect of the rule for predefined operators is simply that x op= y is permitted if both x op y and x = y are permitted. In the example

```
byte b = 0;
char ch = '\0';
int i = 0;

b += 1;            // Okay
b += 1000;         // Error: b = 1000 not permitted
b += i;            // Error: b = i not permitted
b += (byte)i;      // Okay

ch += 1;           // Error: ch = 1 not permitted
ch += (char)1;     // Okay
```

the intuitive reason for each error is that a corresponding simple assignment would also have been an error.

This also means that compound assignment operations support lifted operations. In the example

```
int? i = 0;
i += 1;            // Ok
```

the lifted operator +(int?, int?) is used.

# 7.17.3 Event Assignment

If the left operand of a += or -= operator is classified as an event access, then the expression is evaluated as follows: