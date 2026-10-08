![](bbox=[0.22, 0.08, 0.52, 0.24])

# FIGURE 4.4 The if-else construct

and store them in u and v respectively. Otherwise, find x-y and increment w by 4, and store them in z and w respectively. Finally, compute x*y, and store it in t.

```
```
unsigned char t, u, v, w, x, y, z;
if    (x < y) {
    u = x + y;                  // add x with y, and store in u
    v = x / y;                  // divide x by y and store in v
}
else {
    z = x - y;                  // subtract y from x and store result in z
    w +=    4;                  // value of  w  is incremented by 4
}

    t = x * y                   // multiply x by y and store in t
```
```

In the above, if x < y then the statements for u and v in the braces are executed. The statement t = x * y is then executed. If x is not greater than y then only the statements for z and w+= in the braces are executed. The statement for t is then executed. In either case, t = x * y is executed.

# **4.5.5** The switch construct

The syntax for the switch expression is

```
```
switch ( integer) {
case 1:
    statements;
    break;
case 2:
    statements;
    break;
---
---
---

case n:
    statements;
}
```
```

In the above, the integer included with the switch statement is compared with each of the integers included with the case statements. If the values match, the statements associated with that case statement are executed. For example, consider switch (2). If