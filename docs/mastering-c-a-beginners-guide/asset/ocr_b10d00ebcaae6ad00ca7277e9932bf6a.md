```
// Class declaration
class Newsco_2
{

    // Main Method
    public static void Main(String []args)
    {
        // calling the display method of
        // class Newsco_1 by using two dot
        // operator as one is use to access
        // the class of first namespace
and
        // another is use to access the
        // static method of class Newsco_1.
        // Termed as fully qualified name
        first.Newsco_1.display();
    }
}
```

The output would then be the following:

+   - Hello Newsco!

It is not actually practical to call the function or class (or any other members of a namespace) every time by using its fully qualified name. In the above example, System.Console.WriteLine("Hello Newsco!"); and first.Newsco_1.display(); are the fully qualified name. So C# uses a keyword “using” which helps the user to avoid writing fully qualified names every other time. The user has to add the namespace name