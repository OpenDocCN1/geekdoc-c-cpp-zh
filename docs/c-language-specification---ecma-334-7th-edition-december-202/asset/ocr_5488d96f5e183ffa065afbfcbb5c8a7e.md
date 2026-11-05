```
base_access
  : 'base' '.' identifier type_argument_list?
  | 'base' '[' argument_list ']'
  ;
```

A base_access is used to access base class members that are hidden by similarly named members in the current class or struct. A base_access is permitted only in the block of an instance constructor, an instance method, an instance accessor (§12.2.1), or a finalizer. When base.I occurs in a class or struct, I shall denote a member of the base class of that class or struct. Likewise, when base[E] occurs in a class, an applicable indexer shall exist in the base class.

At binding-time, base_access expressions of the form base.I and base[E] are evaluated exactly as if they were written as ((B)this).I and ((B)this)[E], where B is the base class of the class or struct in which the construct occurs. Thus, base.I and base[E] correspond to this.I and this[E], except this is viewed as an instance of the base class.

When a base_access references a virtual function member (a method, property, or indexer), the determination of which function member to invoke at run-time (§12.6.6) is changed. The function member that is invoked is determined by finding the most derived implementation (§15.6.4) of the function member with respect to B (instead of with respect to the run-time type of this, as would be usual in a non-base access). Thus, within an override of a virtual function member, a base_access can be used to invoke the inherited implementation of the function member. If the function member referenced by a base_access is abstract, a binding-time error occurs.

> Note: Unlike this, base is not an expression in itself. It is a keyword only used in the context of a base_access or a constructor_initializer (§15.11.2). end note

# 12.8.15 Postfix increment and decrement operators

```
post_increment_expression
  : primary_expression '++'
  ;
```

```
post_decrement_expression
  : primary_expression '--'
  ;
```

The operand of a postfix increment or decrement operation shall be an expression classified as a variable, a property access, or an indexer access. The result of the operation is a value of the same type as the operand.

If the primary_expression has the compile-time type dynamic then the operator is dynamically bound (§12.3.3), the post_increment_expression or post_decrement_expression has the compile-time type dynamic and the following rules are applied at run-time using the run-time type of the primary_expression.

If the operand of a postfix increment or decrement operation is a property or indexer access, the property or indexer shall have both a get and a set accessor. If this is not the case, a binding-time error occurs.

Unary operator overload resolution (§12.4.4) is applied to select a specific operator implementation.

Predefined ++ and -- operators exist for the following types: sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double, decimal, and any enum type. The predefined ++ operators return the value produced by adding 1 to the operand, and the predefined -- operators return the value produced by subtracting 1 from the operand. In a checked context, if the result of this addition or subtraction is outside the range of the result type and the result type is an integral type or enum type, a System.OverflowException is thrown.