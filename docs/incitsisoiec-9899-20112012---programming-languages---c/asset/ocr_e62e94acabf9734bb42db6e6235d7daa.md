# int table[TABLESIZE];

EXAMPLE 2 The defining function-like macro whose is the maximum of its arguments. It has the advantages of working for compatible types of arguments and of generating-inline code without the overhead of function calling. It has the disadvantages of evaluating one or the other of it a second time (including side effects) and generating more code than invoked several times. It also cannot have its address, as it has,

```
#define max(a, b) ((a) > (b) ? (a) : (b))
```

The parentheses ensure that the arguments and the resulting expression are bound properly.

EXAMPLE 3 To illustrate the rules for redefinition and reexamination, the sequence

```
#define x 3
#define f(a) f(x * (a))
#undef x
#define x 2
#define g f
#define z z[0]
#define h g(~)
#define m(a) a(w)
#define w 0,1
#define t(a) a
#define p() int
#define q(x) x
#define r(x,y) x ##y
#define str(x) #x
```

```
f(y+1) + f(f(z)) % t(t(g) (0) + t(1);
g(x+(3,4)-w) | h 5 & m
f(f)^m
pi i[q()] = { q(1), r(2,3), r(4), r(5), r(); }
char c[6] = { "str(str, str); };
```

results in

```
f2 (* (y+1)) + f2 (* f2 (* (z(0)))) % f2 (* (0)) + t(1);
f2 (* (2+3,4)-0,1)) | f2 (* (~5) & f2 (* (0,1))^m(0,1);
t i[] = { 1, 23, 4, 5, };
char c[6] = { "hello", " };
```

EXAMPLE 4 To illustrate the rules for creating string literals and concatenating tokens, the sequence

```
#define str(s) #s
#define xstr(str) str(str)
#define debug(s, t) printf("" # s = %d, x" # t = "%s",\n\ x ## s, x ## t)
#define INCFILE(n) vers ## n
#define glue(a, b) a ## b
#define xglue(a, b) glue(a,b)
#define HIGLOW "hello"
#define LOW "world",
```