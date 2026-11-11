be as versatile as Ada's tasks. The availability of the concurrent collection classes is another advantage C# has over the other nonfunctional languages discussed in this chapter.

# ## 13.9 Concurrency in Functional Languages

This section provides a brief overview of support for concurrency in several functional programming languages.

# ### 13.9.1 Multi-LISP

Multi-LISP (Halstead, 1985) is an extension to Scheme that allows the programmer to specify program parts that can be executed concurrently. These forms of concurrency are implicit; the compiler is simply telling the compiler (or interpreter) some parts of the program that can be run concurrently.

One of the ways a programmer can tell the system about possible concurrency is the `pcall` construct. If a function call is embedded in a `pcall` construct, the parameters to the function can be evaluated concurrently. For example, consider the following `pcall` construct:

```
```
(pcall f a b c d)
```
```

The function is f, with parameters a, b, c, and d. The effect of `pcall` is that the parameters of the function can be evaluated concurrently (any or all of the parameters could be complicated expressions). Unfortunately, whether this process can be safely used, that is, without affecting the semantics of the function evaluation, is the responsibility of the programmer. This is actually a simple matter if the language does not allow side effects or if the programmer designed the function not to have side effects or at least to have limited ones. However, Multi-LISP does allow some side effects. If the function was not written to avoid side effects, it may be difficult for the programmer to determine whether `pcall` can be safely used.

The `future` construct of Multi-LISP is a more interesting and potentially more productive source of concurrency. As with `pcall`, a function call is wrapped in a `future` construct. Such a function is evaluated in a separate thread, with the parent thread continuing its execution. The parent thread continues until it needs to use the return value of the function. If the function has not completed its execution when its result is needed, the parent thread waits until it has before it continues.

If a function has two or more parameters, they can also be wrapped in `future` constructs, in which case their evaluations can be done concurrently in separate threads.

These are the only additions to Scheme in Multi-LISP.