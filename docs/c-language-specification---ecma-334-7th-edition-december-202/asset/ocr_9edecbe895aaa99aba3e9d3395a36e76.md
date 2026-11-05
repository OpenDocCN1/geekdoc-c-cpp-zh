```
delegate void D();

class Test
{
    static void F()
    {
        D d = () => Console.WriteLine("test");
    }
}
```

This can be translated to a delegate instantiation that references a compiler generated static method in which the code of the anonymous function is placed:

```
delegate void D();

class Test
{
    static void F()
    {
        D d = new D(__Method1);
    }

    static void __Method1()
    {
        Console.WriteLine("test");
    }
}
```

In the following example, the anonymous function references instance members of this:

```
delegate void D();

class Test
{
    int x;

    void F()
    {
        D d = () => Console.WriteLine(x);
    }
}
```

This can be translated to a compiler generated instance method containing the code of the anonymous function:

```
delegate void D();

class Test
{
    int x;

    void F()
    {
        D d = new D(__Method1);
    }

    void __Method1()
```