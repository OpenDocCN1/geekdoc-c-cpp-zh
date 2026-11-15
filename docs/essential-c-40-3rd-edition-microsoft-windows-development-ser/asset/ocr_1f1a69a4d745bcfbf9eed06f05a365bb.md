```
{
    throw new ArgumentException(
        "numbers cannot be empty");
    }

    int result;
    result = numbers[0];
    foreach (int number in numbers)
    {
        if (number < result)
            result = number;
    }

    return result;
}
```

This class does not have any instance fields (or methods), and therefore, creation of such a class would be pointless. Because of this, the class is decorated with the static keyword. The static keyword on a class provides two facilities. First, it prevents a programmer from writing code that instantiates the SimpleMath class. Second, it prevents the declaration of any instance fields or methods within the class. Since the class cannot be instantiated, instance methods would be pointless.

One more distinguishing characteristic of the static class is that the C# compiler automatically marks it as abstract and sealed within the CIL. This designates the class as inextensible; in other words, no class can be derived from it or instantiate it.

# Extension Methods

Consider the System.IO.DirectoryInfo class which is used to manipulate filesystem directories. The class supports functionality to list the files and subdirectories (DirectoryInfo.GetFiles()) as well as the capability to move the directory (DirectoryInfo.Move()). One feature it doesn't support directly is copy. If you needed such a method you would have to implement it, as shown earlier in Listing 5.37.

The DirectoryInfoExtension.Copy() method is a standard static method declaration. However, notice that calling this Copy() method is different from calling the DirectoryInfo.Move() method. This is unfortunate. Ideally, we