The variadic definition of `output` contains . . . three times, each with a different meaning.

At the beginning, the operator appears in the list of formal template parameters:

```
template<typename First, typename ... Rest>
```

Here, it means that besides the `First` type parameter, there can be zero to any number of additional formal type parameters. They are collectively referred to as `Rest` and can be addressed as such in the template definition.

Then follows . . . in the function header:

```
void output(std::ostream &os, First first, Rest ... rest) {
```

Here . . . stands between the formal type name and the name of the parameter `rest`. This stands for a whole list of parameters—all those after `first`. This is called a *parameter pack*.

In the function body, you can then “unpack” this parameter pack by using the `rest` variable followed by . . .:

```
output(os, rest ...);
```

The compiler then turns this into a sequence of actual parameters at the moment of concrete use.

The important thing here is that `first` no longer appears. As you can see, it is a recursive call to `output`. Without `first`, the list of parameters is one shorter. The list is recursively shortened until there is only a single arbitrary parameter, because then the nonvariadic template fits. Its call ends the recursion.

Specifically, this means that the variadic call leads to a chain of the following calls:

```
// Call:
output(std::cout, "end", 2, 3.14, 'A', false);
// 1st Pass:
output(std::cout, "end");
output(std::cout, 2, 3.14, 'A', false);
// 2nd Pass
output(std::cout, 2);
output(std::cout, 3.14, 'A', false);
// 3rd Pass
output(std::cout, 3.14);
output(std::cout, 'A', false);
// 4th Pass
output(std::cout, 'A');
output(std::cout, false);
```