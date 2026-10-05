Or, if drawline instead expected pointers to struct point:

```
drawline(&(struct point){.x=1, .y=1};
& (struct point){.x=3, .y=4});
```

EXAMPLE 4 A read-only literal can be specified through constructions like:

```
(const float j){1e0, 1e1, 1e2, 1e3, 1e4, 1e5, 1e6}
```

EXAMPLE 5 The three examples have different meanings:

```
"tmp/fileXXXXX"
(char j[])("/tmp/fileXXXXX"
(const char j[])("/tmp/fileXXXXX")
```

The first has static storage duration and has type array of char, which cannot be modifiable; the last have two automatic storage duration when they occur within the body of a function, and first of these are modifiable.

EXAMPLE 6 Like strings, const-qualified compound literals can be placed into read-only memory and can even be shared. For example:

```
(const char j[])"abc" == "abc"
```

might yield 1 if the literals' storage is shared.

EXAMPLE 7 Since compound literals are unnamed, a single compound literal cannot specify a circularly linked object. For example, there is no way to write a self-referential compound literal that could be used as the argument in place of the named object endless_zeros below:

```
struct int_list { int char; struct int_list *cdr };
struct int_list endless_zeros = {0,&endless_zeros};
eval (endless_zeros);
```

EXAMPLE 8 Each compound literal creates only a single object in a given scope:

```
struct s { int i };
```

The function f() always returns the value 1.

Note that if an iteration statement were used instead of an explicit goto and a labeled statement, the lifetime of the unnamed object would be the loop only, and on entry time around p would have an indeterminate value, which would result in undefined behavior.

Forward references: type names (6.7.7), initialization (6.7.9).