```
{
    public void DoSomething()
    {
        // useful code not shown
    }

    public void Dispose()
    {
        // useful code not shown
    }
}
```

Second, widget users can now signal their desire to have the compiler automatically generate the requisite exception handling construct that was shown a moment ago by leveraging the using construct shown here.

```
public interface IDisposable
{
    void Dispose();
}
```

To leverage this construct, the disposable type that was previously instantiated just above the try block is relocated to within the parentheses, and the code that was previously enclosed within the try block is simply located within the curly braces of this new using construct.