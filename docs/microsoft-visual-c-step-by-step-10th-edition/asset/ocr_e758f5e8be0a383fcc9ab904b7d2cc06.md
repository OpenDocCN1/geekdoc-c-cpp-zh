# Declaring an enumeration

You define an enumeration by using the enum keyword followed by a set of symbols identifying the legal values that the type can have enclosed within braces. Here's how you declare an enumeration named Season whose literal values are limited to the names Spring, Summer, Fall, and Winter.

Click here to view code image

```
enum Season { Spring, Summer, Fall, Winter }
```

# Using an enumeration

After you've declared an enumeration, you can use it in the same way you do any other type. If the name of your enumeration is Season, you can create variables of type Season, fields of type Season, and parameters of type Season, as shown in this example:

Click here to view code image

```
enum Season { Spring, Summer, Fall, Winter }
class Example
{
    public void Method(Season parameter) // method parameter example
    {
        Season localVariable; // local variable example
        ...
    }
    private Season currentSeason; // field example
}
```

Before you can read the value of an enumeration variable, it must be assigned a value. You can assign a value that is defined by the enumeration only to an enumeration variable, as illustrated here:

Click here to view code image

```
Season colorful = Season.Fall;
Console.WriteLine(colorful); // writes out 'Fall'
```