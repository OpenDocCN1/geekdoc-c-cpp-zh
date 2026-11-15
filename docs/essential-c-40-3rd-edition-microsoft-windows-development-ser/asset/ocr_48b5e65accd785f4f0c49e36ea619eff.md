# Lambda Expressions

Introduced in C# 3.0, lambda expressions are a more succinct syntax of **anonymous functions** than anonymous methods, where _anonymous functions_ is a general term that includes both lambda expressions and anonymous methods. Lambda expressions are themselves broken into two types: statement lambdas and expression lambdas. Figure 12.2 shows the hierarchical relationship between the terms.

![](bbox=[0.106, 0.3, 0.48, 0.5])

As mentioned earlier in the context of delegates, all anonymous functions are immutable.

# Statement Lambdas

With statement lambdas, C# 3.0 provides a reduced syntax for anonymous methods, a syntax that does not include the delegate keyword and adds the lambda operator, =>. Listing 12.15 shows equivalent functionality to Listing 12.12, except that Listing 12.15 uses a statement lambda rather than an anonymous method.

```
LISTING 12.15: Passing a Delegate with a Statement Lambda

class DelegateSample
{
    // ...
```