# Try It Yourself

# Working with Methods

Continuing to expand the Contact class, add the VerifyEmailAddress and Search methods by following these steps. If you closed Visual Studio, repeat the previous exercises first. Be sure to keep Visual Studio open at the end of this exercise because you will use this application later.

+   1. Open the Contact.cs file.

+   2. Add the VerifyEmailAddress method shown in Listing 3.6 so that it returns true if the email address entered is “joe@example.com”.

+   3. Add the overloaded methods shown in Listing 3.7.

+   4. In the last overloaded Search method, enter a Console.WriteLine call that prints the values of the parameters.

+   5. In the Main method of the Program.cs file, enter the following code after the last Console.WriteLine statement:

```
c.Search(37.479444f, -122.450278f);
c.Search(37.479444f, -122.450278f, 50);
c.Search(37.479444f, -122.450278f, 50, "on");

Console.WriteLine(c.VerifyEmailAddress("joe@example.com"));
Console.WriteLine(c.VerifyEmailAddress("jim@example.com"));
```

+   6. Run the application using Ctrl+F5 and observe that the output matches what is shown in Figure 3.5.

![](bbox=[0.05, 0.63, 0.75, 0.75])

# Optional Parameters and Named Arguments

Optional parameters enable you to omit that argument in the invocation list when calling a method. Only value parameters can be optional, and all optional parameters must appear after required parameters, but before a parameter array.

To declare a parameter as optional, you simply provide a default value for it. The modified Search method using optional parameters is shown here: