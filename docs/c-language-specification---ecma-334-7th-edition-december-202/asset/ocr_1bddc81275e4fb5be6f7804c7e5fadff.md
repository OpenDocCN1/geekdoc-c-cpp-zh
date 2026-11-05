```
F1();
// OK, F3 reads s2, which is definitely assigned in F2.
F3();

void F1()
{
    Console.WriteLine(s);
}

void F2()
{
    i = 5;
    // OK. i is definitely assigned.
    Console.WriteLine(i);
    s2 = i.ToString();
}

void F3()
{
    Console.WriteLine(s2);
}
```

end example

# 9.4.4.34 is-pattern expressions

For an expression expr of the form:

expr_operand is pattern

+   - The definite-assignment state of v before expr_operand is the same as the definite-assignment state of v before expr.
+   - If the variable ‘v’ is declared in pattern, then the definite-assignment state of ‘v’ after expr is “definitely assigned when true”.
+   - Otherwise the definite assignment state of ‘v’ after expr is the same as the definite assignment state of ‘v’ after expr_operand.

# 9.5 Variable references

A variable_reference is an expression that is classified as a variable. A variable_reference denotes a storage location that can be accessed both to fetch the current value and to store a new value.

```
variable_reference
: expression
;
```

Note: In C and C++, a variable_reference is known as an lvalue. end note

# 9.6 Atomicity of variable references

Reads and writes of the following data types shall be atomic: bool, char, byte, sbyte, short, ushort, uint, int, float, and reference types. In addition, reads and writes of enum types with an underlying type in