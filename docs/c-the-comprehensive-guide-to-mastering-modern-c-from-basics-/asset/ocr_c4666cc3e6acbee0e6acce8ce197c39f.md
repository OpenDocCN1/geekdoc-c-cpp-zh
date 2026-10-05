In the nonvariadic case, there is nothing new—namely,
no three dots ....

At the beginning, the operator appears in the list of
formal template parameters:

```
template<typename First, typename ... Rest>
```

Then follows ... in the function header:

```
void output(std::ostream& os, First first, Rest ... rest) {
```

Here ... stands between the formal type name and the
name of the parameter rest. This stands for a whole list
of parameters—all those after first. This is called a
parameter pack.

In the function body, you can then “unpack” this
parameter pack by using the rest variable followed by
...

```
output(os, rest ...);
```