be used on another branch of an **if**-statement. For example:

```
void f2(int i)
{
if (i) { int x = i+2;
++x;
// ...
}
else {
++x; // error :xisnot in scope
}
++x; // error :xisnot in scope
}
```

A branch of an **if**-statement cannot be just a declaration. If we need to introduce a name in a branch, it must be enclosed in a block (§9.2). For example:

```
void f1(int i) {
if (i) int x = i+2; // error :declaration of if-statement branch }
```

# 9.4.2 switch Statements

A **switch**-statement selects among a set of alternatives (**case**-labels). The expression in the **case** labels must be a constant expression of integral or enumeration type. A value may not be used more than once for **case**-labels in a **switch**-statement. For example:

```
void f(int i)
{
switch (i) {
case 2.7: // error :floating point uses for case
// ...
case 2:
// ...
case 4-2: // error :2used twice in case labels
// ...
};
```

A **switch**-statement can alternatively be written as a set of **if**-statements. For example:

```
switch (val) {
case 1:
f();
break;
case 2:
g();
break;
default:
h();
```