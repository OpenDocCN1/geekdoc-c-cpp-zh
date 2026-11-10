# 7.3  ACCESS TO NONLOCAL DATA ON THE STACK

```
```c
int f(int n) {
    int t, s;
    if (n < 2) return 1;
    s = f(n-1);
    t = f(n-2);
    return s+t;
}
```
```

Figure 7.9: Fibonacci program for Exercise 7.2.3

+   a) Which function creates the space on the stack for each element?
+   
+   b) Which function writes the value of each element?
+   
+   c) To which activation record does the element belong?

**Exercise 7.2.5:** In a language that passes parameters by reference, there is a function $f(x, y)$ that does the following:

```
```text
x = x + 1; y = y + 2; return x+y;
```
```

If $a$ is assigned the value 3, and then $f(a,a)$ is called, what is returned?

**Exercise 7.2.6:** The C function $f$ is defined by:

```
```c
int f(int x, *py, **ppz) {
    **ppz += 1; *py += 2; x += 3; return x+*py+***ppz;
}
```
```

Variable $a$ is a pointer to $b$; variable $b$ is a pointer to $c$, and $c$ is an integer currently with value 4. If we call $f(c,b,a)$, what is returned?

# 7.3  Access to Nonlocal Data on the Stack

In this section, we consider how procedures access their data. Especially important is the mechanism for finding data used within a procedure $p$ but that does not belong to $p$. Access becomes more complicated in languages where procedures can be declared inside other procedures. We therefore begin with the simple case of C functions, and then introduce a language, ML, that permits both nested function declarations and functions as “first-class objects;” that is, functions can take functions as arguments and return functions as values. This capability can be supported by modifying the implementation of the run-time stack, and we shall consider several options for modifying the activation records of Section 7.2.