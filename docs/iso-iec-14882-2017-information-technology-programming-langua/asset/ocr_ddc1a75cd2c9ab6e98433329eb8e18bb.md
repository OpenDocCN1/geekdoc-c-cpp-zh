# ISO/IEC 14882:2017(E)

10 [Note: Every object of static storage duration is zero-initialized at program startup before any other initialization takes place. In some cases, additional initialization is done later. — end note]

11 An object initializer is an empty set of parentheses, i.e., shall be value-initialized.

> [Note: Since (O) is not permitted by the syntax for initializer,
X a; is not the declaration of an object of class X, but the declaration of a function taking no argument and returning X. The is permitted in certain initialization contexts (8.3.4, 8.2.3, 15.6.2). — end note]

12 If no initializer is specified for an object, the object is de-initialized. When an object with automatic or dynamic storage duration is initialized, the object has an indeterminate value, and if no initialization is performed, the object has an indeterminate value until it is replaced (8.18). [Note: Objects with static or storage duration are zero-initialized, 6.6.2. — end note]
An indeterminate value is produced by an evaluation, the behavior is undefined except in the following cases:

+   (12.1) An indeterminate value of unsigned narrow character type (6.9.1) and std::byte type (21.2.1) is produced by the evaluation of:

+   (12.1.1) the second or third operand of a conditional expression (8.16),

+   (12.1.2) the right operand of a comma expression (8.19),

+   (12.1.3) the operand of a cast or conversion (7.8, 8.2.3, 8.2.9, 8.4) to an unsigned narrow character type or std::byte type (21.2.1), and

+   (12.1.4) a discarded-value expression (Clause 8),

then the value of the expression is an indeterminate value.

(12.2) If an indeterminate value of unsigned narrow character type or std::byte type is produced by the evaluation of a simple assignment object (8.18) whose first operand is an value of unsigned narrow character type or std::byte type, an indeterminate value replaces the value of the object referred to by the left operand.

(12.3) If an indeterminate value of unsigned narrow character type is produced by the evaluation of the initialization expression when initializing an object of unsigned narrow character type, that object is initialized to an indeterminate value.

(12.4) If an indeterminate value of unsigned narrow character type or std::byte type is produced by the evaluation of the initialization expression when initializing an object of std::byte type, that object is initialized to an indeterminate value.

[Example:

```
int func(bool b) {
    unsigned char c;
    unsigned char d = c;
    int e = d; // d has an indeterminate value
    return b ? d : e; // undefined behavior
                   // undefined behavior if b is true
}
```

— end example]

13 An initializer for a static member is in the scope of the member's class. [Example:

int a;

struct X {
    static int a;