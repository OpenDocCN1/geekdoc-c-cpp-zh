![](bbox=[0.11, 0.08, 0.88, 0.46])

Figure 12.2 – Graph of the function $f$.

```
```text
....:        yield u
....:        if f(u) * f(s) < 0:
....:            t = u
....:        else:
....:            s = u
```
```

The definition of this function deserves explanation. The keyword `yield` in the definition of `intervalgen` turns it into a *generator* (see §15.2.4). When the method `next()` of a generator is called, if the interpreter sees the keyword `yield`, all local data are saved, the execution is interrupted and the expression immediately at the right of the keyword is returned. The following call of the method `next()` restores the local data that was saved before the interruption and continues from the line following the keyword `yield`. The usage of the keyword `yield` inside an infinite loop (`while True:`) allows the implementation of a recursive sequence via a syntax that resembles closely its mathematical definition. It is possible to stop the execution completely by using the keyword `return`.

The parameter `phi` is a function that specifies the approximation method. For the bisection method, this function computes the midpoint of an interval. In order to test other iterative approximation methods that also use nested intervals, we need to give a new definition of the function `phi` and can then use the function `intervalgen` to construct the corresponding generator.

The parameters `s` and `t` of the function specify the endpoints of the first