# Part I: C# Fundamentals

Another use of explicit interface member implementation occurs when two interfaces have the same method name but different signatures. For example:

```
public interface IFileLogging
{
    void LogError(string str);
}

public interface IConsoleLogging
{
    void LogError();
}
```

Here, the LogError() method in the IFileLogging interface has a string input parameter, while there is no parameter in the IConsoleLogging interface. When you now implement the two interfaces, you can provide two overloaded LogError() methods, together with an implementation specific to each interface as illustrated here:

```
public class Calculation : IFileLogging, IConsoleLogging
{
    //---common to both interfaces---
    public void LogError(string str)
    {
        Console.WriteLine("In LogError(str): " + str);
    }
    public void LogError()
    {
        Console.WriteLine("In LogError()");
    }

    //---only available to the IFileLogging interface---
    void IFileLogging.LogError(string str)
    {
        Console.WriteLine("In IFileLogging: " + str);
    }

    //---only available to the IConsoleLogging interface---
    void IConsoleLogging.LogError()
    {
        Console.WriteLine("In IConsoleLogging");
    }
}
```

As you can see , the first two LogError() methods are overloaded and are common to both interfaces. This means that you can access them via an instance of the Calculation class. The next two implementations are specific to the IFileLogging and IConsoleLogging interfaces and can be accessed only via an instance of each interface:

```
//---create an instance of Calculation---
Calculation c = new Calculation();

//---prints out: In LogError()---
```