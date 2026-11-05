```
overloadable-binary-operator:
  +
  -
  *
  /
  %
  &
  |
  ^
  <<
  right-shift
  ==
  !=
  >
  <
  >=
  <=

conversion-operator-declarator:
  implicit operator type ( type identifier )
  explicit operator type ( type identifier )

operator-body:
  block
  ;
```

There are three categories of overloadable operators: Unary operators (§10.10.1), binary operators (§10.10.2), and conversion operators (§10.10.3).

When an operator declaration includes an extern modifier, the operator is said to be an external operator. Because an external operator provides no actual implementation, its operator-body consists of a semi-colon. For all other operators, the operator-body consists of a block, which specifies the statements to execute when the operator is invoked. The block of an operator must conform to the rules for value-returning methods described in §10.6.10.

The following rules apply to all operator declarations:

+   - An operator declaration must include both a public and a static modifier.
+   - The parameter(s) of an operator must be value parameters. It is a compile-time error for an operator declaration to specify ref or out parameters.
+   - The signature of an operator (§10.10.1, §10.10.2, §10.10.3) must differ from the signatures of all other operators declared in the same class.
+   - All types referenced in an operator declaration must be at least as accessible as the operator itself (§3.5.4).
+   - It is an error for the same modifier to appear multiple times in an operator declaration.

Each operator category imposes additional restrictions, as described in the following sections.

Like other members, operators declared in a base class are inherited by derived classes. Because operator declarations always require the class or struct in which the operator is declared to participate in the signature of the operator, it is not possible for an operator declared in a derived class to hide an operator declared in a base class. Thus, the new modifier is never required, and therefore never permitted, in an operator declaration.

Additional information on unary and binary operators can be found in §7.3.