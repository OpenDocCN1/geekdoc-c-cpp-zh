# 9.4.1 if Statements

In an if-statement, the first (or only) statement is executed if the condition is true and the second statement (if it is specified) is executed otherwise. If a condition evaluates to something different from a Boolean, it is – if possible – implicitly converted to a bool. This implies that any arithmetic or pointer expression can be used as a condition. For example, if x is an integer, then

```
if (x) // ...
means
if (x != 0) // ...
```

For a pointer p,

```
if (p) // ...
```

is a direct statement of the test “Does p point to a valid object (assuming proper initialization)?” and is equivalent to

```
if (p != nullptr) // ...
```

Note that a “plain” enum can be implicitly converted to an integer and then to a bool, whereas an enum class cannot (§8.4.1). For example:

Section 9.4.1 ifStatements 229

```
enum E1 { a, b };
enum class E2 { a, b };
void f(E1 x, E2 y) {
if (x) // OK
// ...
if (y) // error :no conversion to bool
// ...
if (y==E2::a) // OK
// ...
}
```

The logical operators

```
&& || !
```

are most commonly used in conditions. The operators && and || will not evaluate their second argument unless doing so is necessary. For example,

```
if (p && 1<p->count) // ...
```

This tests 1<p->count only if p is not nullptr.

For choosing between two alternatives each of which produces a value, a conditional expression (§11.1.3) is a more direct expression of intent than an if-statement. For example:

```
int max(int a, int b)
{
return (a>b)?a:b; // returnthe larger of a and b
}
```

A name can only be used within the scope in which it is declared. In particular, it cannot