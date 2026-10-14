IDisposable interface, as shown here in bold:

Click here to view code image

```
class Calculator : IDisposable
{
    ...
}
```

3. Add to the end of the Calculator class the following method (named Dispose). This method is defined by the IDisposable interface:

Click here to view code image

```
class Calculator : IDisposable
{
    ...
    public void Dispose()
    {
        Console.WriteLine("Calculator being disposed");
    }
}
```

You would normally add code to the Dispose method that releases the resources held by the object. There are none in this case, and the purpose of the Console.WriteLine statement in this method is just to let you see when the Dispose method is run. However, you can see that in a real-world application, there would likely be some duplication of code between the destructor and the Dispose method. To remove this duplication, you would typically place this code in one place and call it from the other. But because you cannot explicitly invoke a destructor from the Dispose method, it makes sense instead to call the Dispose method from the destructor and place the logic that releases resources in the Dispose method.

4. Modify the destructor so that it calls the Dispose method, as shown in bold in the following code. (Leave the statement displaying the message in place in the finalizer so that you can see when it is being run by the garbage collector).

Click here to view code image

```
~Calculator()
{
    Console.WriteLine("Calculator being finalized");
    this.Dispose();
}
```

When you want to destroy a Calculator object in an application, the Dispose method does not run automatically; your code must either call it explicitly (with a statement such as calculator.Dispose()) or create the Calculator object within a using statement. In your program, you will adopt the latter approach.