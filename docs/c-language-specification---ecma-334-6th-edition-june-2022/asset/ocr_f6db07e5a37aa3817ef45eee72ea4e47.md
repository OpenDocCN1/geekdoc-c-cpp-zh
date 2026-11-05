+   - A negative infinity is considered less than all other values, but equal to another negative infinity.
+   - A positive infinity is considered greater than all other values, but equal to another positive infinity.

Lifted (§11.4.8) forms of the unlifted predefined floating-point comparison operators defined above are also predefined.

# 11.11.4 Decimal comparison operators

The predefined decimal comparison operators are:

```
bool operator ==(decimal x, decimal y);
bool operator !=(decimal x, decimal y);
bool operator <(decimal x, decimal y);
bool operator >(decimal x, decimal y);
bool operator <=(decimal x, decimal y);
bool operator >=(decimal x, decimal y);
```

Each of these operators compares the numeric values of the two decimal operands and returns a bool value that indicates whether the particular relation is true or false. Each decimal comparison is equivalent to using the corresponding relational or equality operator of type System.Decimal.

Lifted (§11.4.8) forms of the unlifted predefined decimal comparison operators defined above are also predefined.

# 11.11.5 Boolean equality operators

The predefined Boolean equality operators are:

```
bool operator ==(bool x, bool y);
bool operator !=(bool x, bool y);
```

The result of == is true if both x and y are true or if both x and y are false. Otherwise, the result is false.

The result of != is false if both x and y are true or if both x and y are false. Otherwise, the result is true. When the operands are of type bool, the != operator produces the same result as the ^ operator.

Lifted (§11.4.8) forms of the unlifted predefined Boolean equality operators defined above are also predefined.

# 11.11.6 Enumeration comparison operators

Every enumeration type implicitly provides the following predefined comparison operators

```
bool operator ==(E x, E y);
bool operator !=(E x, E y);
bool operator <(E x, E y);
bool operator >(E x, E y);
bool operator <=(E x, E y);
bool operator >=(E x, E y);
```

The result of evaluating x «op» y, where x and y are expressions of an enumeration type E with an underlying type U, and «op» is one of the comparison operators, is exactly the same as evaluating ((U)x) «op» ((U)y). In other words, the enumeration type comparison operators simply compare the underlying integral values of the two operands.

Lifted (§11.4.8) forms of the unlifted predefined enumeration comparison operators defined above are also predefined.