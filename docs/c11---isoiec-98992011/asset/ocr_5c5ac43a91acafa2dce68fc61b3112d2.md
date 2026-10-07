# © ISO/IEC 2011 – All rights reserved
ISO/IEC 9899:2011 (E)

Or, if drawline expected pointers to struct point:

```
drawline (&struct point){.x=1, .y=1},
&(&struct point){.x=3, .y=4});
```

11 EXAMPLE 4 A read-only literal can be specified through constructions like:

```
(const float (1))e0, e1, e2, e3, e4, e5, e6)
```

12 EXAMPLE 5 The three expressions have different meanings:

```
"/tmp/fileXXXXXX"
(char []) "/tmp/fileXXXXXX"
(const char (1))"/tmp/fileXXXXXX"
```

The first always has static storage and has type array of char, which are not modifiable; the last two have automatic storage when they occur within the body of the function, and the first of these are modifiable.

13 EXAMPLE 6 Like strings, const-qualified compound literals can be linked into read-only memory and can be ended. For example:

```
(const char [1])"abc" == "abc"
might might yield 1 if the literal's storage is shared.
```

14 EXAMPLE 7 Since compound literals are unnamed, a single compound literal cannot specifically a linked object. there is no way to write a self-referential compound literal that could be used as the function argument in the place of the object endless_zeros below:

```
struct int_list { int char; struct int_list *cdr };
struct int_list endless_zeros = {0, &endless_zeros};
eval(endless_zeros);
```

15 EXAMPLE 8 Each compound literal creates only a single object in a given scope:

```
struct s { int i; }
int f (void)
{
struct s *p = 0, *q;
int j = 0;
again:
p = p, p = &((struct s){ j++ });
q (j < 2) goto again;
return p == q && q->i == 1;
}
```

The function f() returns the value 1.

16 Note that if an iteration statement were used instead of an explicit goto to the body of the loop, and on next time around p would have an indeterminate value, which would result in undefined behavior.

Forward references: type names (6.7.7), initialization (6.7.9).

§6.5.2.5                               Language 87