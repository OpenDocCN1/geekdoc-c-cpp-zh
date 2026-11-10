+   7.9  Multiple **case** options in **switch** can have a single **break**.
+   7.10  The keyword **default** must be used as the last option of a **switch** construct.

# A2.  FILL IN THE BLANKS

+   7.1  The sequence (x > 3) in **if (x > 3)** is known as a ______ ______.
+   7.2  A compound statement must be enclosed by ______ ______.
+   7.3  A solitary ; placed on a line signifies a ______ statement.
+   7.4  The ______ keyword prevents control from falling through in a **switch** construct.
+   7.5  The expression matched by **switch** must evaluate to an ______ value.
+   7.6  The ______ statement doesn’t return to the place from where it was executed.
+   7.7  A conditional expression comprises a ______ operator that uses the symbols ______ and ______.

# A3.  MULTIPLE-CHOICE QUESTIONS

+   7.1  Of the two operators, && and ||, the && has a (A) higher priority, (B) lower priority, (C) same priority.

+   7.2  Use of curly braces ({ }) for enclosing the body of the **if** statement is (A) optional, (B) recommended, (C) compulsory when executing at least two statements, (D) compulsory in a nested or ladder **if** structure, (E) C and D.

+   7.3  Consider the following code:

```
int x = 5;
if (x++ == 10)
    x = 0;
else
    ++x;
```

The final value of x is (A) 5, (B) 6, (C) 7, (D) implementation-dependent.

+   7.4  Consider the following code:

```
int x = 5;
if (x = 6)
    x = 0;
else
    x = 10;
```

The value of x is (A) 10, (B) 0, (C) 5, (D) 6.

+   7.5  Select the odd operator out: (A) &&, (B) ||, (C) !=, (D) !.

+   7.6  Consider the following code:

```
int x = 5;
x = x == 5 ? 1 : 10;
```

The value of x is (A) 1, (B) 5, (C) 10, (D) implementation-dependent.