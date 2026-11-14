Then it will be evaluated as

```
int max_result= a+b*a+b >= a-b*a ? a+b*a+b : a-b*a-b;
```

yielding evidently wrong results. This problem can be fixed with some parentheses:

```
#define max_square(x, y) ((x)*(x) == (y)*(y) ? (x)*(x) : (y)*(y))
```

To protect against high-priority operators, we also surrounded the entire expression with a pair of parentheses. Thus, macro expressions need parentheses around each argument and around the entire expression. Note that this is necessary, not a sufficient, condition for correctness.

Another serious problem is the replication of arguments in expressions. If we call `max_square` as in

```
int max_result= max_square(++a, ++b);
```

the variables a and b are incremented four times.

Macros are a quite simple language feature, but implementing and using them is more complicated and dangerous than it seems at first glance. The hazard is that they interact with the entire program. Therefore, new software should not contain macros at all. Unfortunately, existing software already contains many of them and we have to deal with them.

Regrettably, there is no general cure for trouble with macros. Here are some tips that work in most cases:

+   Avoid names of popular macros. Most prominently, assert is a macro in the standard library and giving that name to a function is asking for trouble.

+   Undefine the macro with `#undef`.

+   Include macro-heavy libraries after all others. Then the macros still pollute your application but not the other included header files.

+   Impressively, some libraries offer protection against their own macros: one can define a macro that disables or renames macros' dangerously short names.²

# ## A.3 Real-World Example: Matrix Inversion

> > "The difference between theory and practice is larger in practice than in theory."

—Tilmar König

To round up the basic features, we apply them to demonstrating how we can easily create new functionality. We want to give you an impression of how our ideas can evolve naturally into reliable and efficient C++ programs. Particular attention is paid to clarity and reusability. Our programs should be well-structured inside and intuitive to use from outside.

2. We have seen a library that defined a single underscore as a macro which created a lot of problems.