compact. An anonymous method must explicitly type every parameter, and must have a statement block. Rather than using the lambda operator `->` between the parameter list and the code block, an anonymous method puts the keyword `delegate` before the parameter list, emphasizing that the anonymous method must be converted to a `delegate` type. Listing 13.17 shows the code from Listings 13.7, 13.12, and 13.15 rewritten to use an anonymous method.

# LISTING 13.17: Passing an Anonymous Method in C# 2.0

```
```
// ...
BubbleSort(items,
    delegate(int first, int second)
    {
        return first < second;
    }
);
// ...
```
```

It is unfortunate that there are two very similar ways to define an anonymous function in C# 3.0 and later.

**Guidelines**  
* AVOID the anonymous method syntax in new code; prefer the more compact lambda expression syntax.

There is, however, one small feature that is supported in anonymous methods that is not supported in lambda expressions: Anonymous methods may omit their parameter list entirely in some circumstances.

# ## ADVANCED TOPIC

# ### Parameterless Anonymous Methods

Unlike lambda expressions, anonymous methods may omit the parameter list entirely provided that the anonymous method body does not use any parameter and the `delegate` type requires only “value” parameters (i.e., it does not require the parameters to be marked as `out` or `ref`). For example, the anonymous method expression `delegate { return Console.ReadLine() != ";"; }` is convertible to

![](bbox=[0.88, 0.72, 0.99, 0.9])