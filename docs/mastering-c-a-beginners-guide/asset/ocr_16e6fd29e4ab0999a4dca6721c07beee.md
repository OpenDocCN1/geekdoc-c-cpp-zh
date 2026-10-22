# Closures

When we are discussing functions, we should talk about the scope of variables. In the standard functions, we have the following types of variables:

+   - Arguments that are passed to the function.
+   - Local variables that are defined and used inside the function body. They are smashed straightaway when function finishes.
+   - Global variables that are defined out of the function and referenced in the function body. These variables live even when the function ends.

If you need to develop a delegate or lambda expression, you should use arguments and local variables, and reference them outside the delegate. Example is shown in the following listing:

```
int val = 0;
Func<int, int> add = delegate(int delta) {
val+=delta; return val; };
val = 10;
var x = add(5);
// val = 15, x = 15
var y = add(7);
// val = 22, y = 22
```

Here, we have developed one delegate that adds the value of the parameter to the variable val that is defined outside the delegate.