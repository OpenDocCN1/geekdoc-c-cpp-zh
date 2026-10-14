# Note

The ToString method is a little different from the methods you have seen so far. Every type, including structures and classes that you define, automatically has a ToString method whether or not you want it. Its default behavior is to convert the data in a variable to a string representation of that data. Sometimes the default behavior is meaningful; other times it is less so. For example, the default behavior of the ToString method generated for the Date structure simply generates the string “StructsAndEnums.Date”. To quote Zaphod Beeblebrox in The Restaurant at the End of the Universe by Douglas Adams (Pan Macmillan, 1980), this is “shrewd, but dull.” You need to define a new version of this method that overrides the default behavior by using the override keyword. Overriding methods are discussed in more detail in Chapter 12.

The ToString method should look like this:

Click here to view code image

```
struct Date
{
    ...
    public override string ToString()
    {
        string data = $"{this.month} {this.day + 1} {this.year + 1900}";
        return data;
    }
}
```

In this method, you build a formatted string using the text representations of the values of the month field, the expression this.day + 1, and the expression this.year + 1900. The ToString method returns the formatted string as its result.

+   5. Display the Program.cs file in the Code and Text Editor window.

+   6. In the doWork method, comment out the four existing statements.

+   7. Add statements to the doWork method that declare a local variable named defaultDate and initialize it to a Date value constructed by using the default Date constructor. Add another statement to doWork to display the defaultDate variable on the console by calling Console.WriteLine.