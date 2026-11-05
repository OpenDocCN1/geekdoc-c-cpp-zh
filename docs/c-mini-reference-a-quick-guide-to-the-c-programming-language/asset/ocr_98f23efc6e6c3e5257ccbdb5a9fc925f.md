# 9.2. Argument List

Invocation of a function or method is an expression.

```
EXPRESSION ( ARGUMENT_LIST )
```

EXPRESSION should be "callable", e.g., a method or a value of a delegate type. ARGUMENT_LIST can be empty. It follows more or less the same structure as the parameter and each given argument must have a corresponding parameter in the parameter list.

C# supports two kinds of argument syntax, positional arguments and named A named argument has a form PARAMETER_NAME : whereas only VALUE is specified for a positional argument. When an argument is in the same position in the argument list as the corresponding parameter in the parameter list, it can use either named or positional argument syntax. Otherwise, only the named argument syntax is allowed. For example, given the following function,

```
static void Metodo(int a = 1, char b = 'b') {
    Console.WriteLine($"a = {a}; b = {b}");
}
```

We can call this function in any of the following ways: