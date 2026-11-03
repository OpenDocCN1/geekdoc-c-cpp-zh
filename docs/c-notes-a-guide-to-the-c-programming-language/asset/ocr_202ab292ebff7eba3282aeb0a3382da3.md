When the else phrase is omitted, it is just as if else /* null */; were explicitly specified. For example,

```
if (k < 2)
 p = f(k);
else
 p = g(2 - k);
```

will perform exactly one of the two assignments depending on the magnitude of k relative to 2. Relational operators deliver a value of 1 for “true” and 0 for “false” as more fully discussed in Chapter 3. A common form is

```
if (p)
...
else if (q)
...
else if (r)
...
else
/* none of the above */
...
```

and this style of indentation is Recommended.

Frequently enough, the logical exprs p, q, r, and so forth, are of the form k == 1, k == 2, k == 5, etc., where == is the equality comparison operator in C. Such cases are catered for by the switch statement as exemplified by

```
switch(k - 2)
{
case 3: j = k*k; break;
case 5, 2: ++k; do_something(k); break;
default: error ("bad k");
}
```

Since the case prefix allows only constant expressions, the switch statement can be implemented very efficiently. The break statements are necessary to terminate the switch statement after each selectable portion; otherwise, control flows from one case to the next in a most unsatisfactory manner. Case labels may occur embedded within a compound statement. Only an embedded switch statement limits this questionable facility.