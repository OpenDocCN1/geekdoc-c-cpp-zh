# ADVANCED TOPIC

# **Strings Are Immutable**

All values of type `string`, whether string literals or otherwise, are immutable (or unmodifiable). For example, it is not possible to change the string `Come As You Are.` to `Come As You Age.` A change such as this requires that you reassign the variable instead of modifying the data to which the variable originally referred.

# ## Console Input and Output

This chapter already used `System.Console.WriteLine` repeatedly for writing out text to the command console. In addition to being able to write out data, a program needs to be able to accept data that a user may enter.

# ### Getting Input from the Console

One way to retrieve text that is entered at the console is to use `System.Console.ReadLine()`. This method stops the program execution so that the user can enter characters. When the user presses the **Enter** key, creating a newline, the program continues. The output, also known as the **return**, from the `System.Console.ReadLine()` method is the string of text that was entered. Consider Listing 1.14 and the corresponding output shown in Output 1.4.

# LISTING 1.14: Using `System.Console.ReadLine()`

```
```csharp
class HeyYou
{
    static void Main()
    {
        string firstName;
        string lastName;

        System.Console.WriteLine("Hey you!");

        System.Console.Write("Enter your first name: ");
        firstName = System.Console.ReadLine();

        System.Console.Write("Enter your last name: ");
        lastName = System.Console.ReadLine();
    }
}
```
```