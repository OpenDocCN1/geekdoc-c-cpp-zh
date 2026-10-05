In short, if a continuation captured by call/cc is ever invoked with some value, then the computation will continue by returning that value as the value of the call to call/cc that captured it and resuming execution normally from there.

# ## Exercise 5.21: Nonlocal exits

This exercise is to be done in the native Scheme, where it will be easier to debug and instrument than in our embedded interpreter. There is a good implementation of call/cc in the native Scheme.

+   a. Define a simple procedure, snark-hunt,29 that takes a tree as its argument and recursively descends the looking for the symbol snark at any leaf. It should immediately stop searching and return #t if one is found; #f otherwise. Use call/cc. For example:

```
(snark-hunt '((a b c) d (e f) g ((snark "oops") h) (i j))))
#t
```

Note that the input to snark-hunt may not be composed solely of proper lists.

+   b. How might you verify that snark-hunt exits immediately rather than silently returning through multiple return values? Define a new procedure, snark-hunt/instrumented, to demonstrate this.

Hint: Setting an exit status flag, then signaling an error on wayward return paths might work if placed carefully, but simply tracing via pp may be easier. Any quick and dirty hack that works will do. The goal is to build your intuition about continuations, not to ship product-quality code. Briefly explain your strategy.

# ### 5.5.2 Nonlocal transfer of control

The preceding was somewhat simplistic, because the continuations captured were used only for nonlocal exits. But continuations are