can be equivalently rewritten as

```
if (x) {
    int i;
}
```

Thus after the if statement, i is no longer in scope. — end example]

# 8.5.2 The if statement [stmt.if]

1 If the condition (8.5) yields true the first substatement is executed. If the else part of the selection statement is present and the condition yields false, the second substatement is executed. If the first substatement is reached via a label, the condition is not evaluated and the second substatement is not executed. In the second form of if statement (the one including else), if the first substatement is also an if statement then that inner if statement shall contain an else part.88

2 If the if statement is of the form if constexpr, the value of the condition shall be a contextually converted constant expression of type bool (7.7); this form is called a constexpr if statement. If the value of the converted condition is false, the first substatement is a discarded statement, otherwise the second substatement, if present, is a discarded statement. During the instantiation of an enclosing templated entity (13.1), if the condition is not value-dependent after its instantiation, the discarded substatement (if any) is not instantiated. [Note 1: Odr-uses (6.3) in a discarded statement do not require an entity to be defined. — end note]

A case or default label appearing within such an if statement shall be associated with a switch statement (8.5.3) within the same if statement. A label (8.2) declared in a substatement of a constexpr if statement shall only be referred to by a statement (8.7.6) in the same substatement.

[Example 1:

```
template<typename T, typename ... Rest> void g(T&& p, Rest&& ...rs) {
    // ... handle p

    if constexpr (sizeof...(rs) > 0)
        g(rs...);        // never instantiated with an empty argument list
}
```

```
extern int x;        // no definition of x required
```

```
int f() {
    if constexpr (true)
        return 0;
    else if (x)
        return x;
    else
        return -x;
}
```

— end example]

3 An if statement of the form

```
if constexpr_opt ( init-statement condition ) statement
```

is equivalent to

```
{
    init-statement
    if constexpr_opt ( condition ) statement
}
```

and an if statement of the form

```
if constexpr_opt ( init-statement condition ) statement else statement
```

is equivalent to

```
{
    init-statement
    if constexpr_opt ( condition ) statement else statement
}
```