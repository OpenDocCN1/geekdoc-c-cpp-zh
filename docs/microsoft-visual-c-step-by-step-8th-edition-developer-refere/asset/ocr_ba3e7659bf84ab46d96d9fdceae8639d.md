The purpose of this field is to track the state of this object and indicate whether the Dispose method has been invoked.

3. Modify the code in the Dispose method to display the message only if the disposed field is false. After displaying the message, set the disposed field to true, as demonstrated here in bold:

Click here to view code image

```
public void Dispose()
{
    if (!this.disposed)
    {
        Console.WriteLine("Calculator being disposed");
    }
    this.disposed = true;
}
```

4. On the Debug menu, click Start Without Debugging. Notice that the program displays the following series of messages:

```
Calculator being created
120 / 15 = 8
Calculator being disposed
Program finishing
Calculator being finalized
```

The Calculator object is now discarded only once, but the destructor is still running. Again, this is a waste; there is little point in running a destructor for an object that has already released its resources.

5. In the console window, press the Enter key and return to Visual Studio 2015.

6. In the Calculator class, add to the end of the Dispose method the following statement shown in bold:

Click here to view code image

```
public void Dispose()
{
    if (!this.disposed)
    {
        Console.WriteLine("Calculator being disposed");
    }
    this.disposed = true;
    GC.SuppressFinalize(this);
}
```

The GC class provides access to the garbage collector, and it implements several static methods with which you can control some of the actions it