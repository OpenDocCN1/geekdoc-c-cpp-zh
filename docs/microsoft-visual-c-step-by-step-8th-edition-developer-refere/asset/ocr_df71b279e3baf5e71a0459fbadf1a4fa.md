| Question | Structure | Class |
|---|---|---|
| Is this a value type or a reference type? | A structure is a value type. | A class is a reference type. |
| Do instances live on the stack or the heap? | Structure instances are called *values* and live on the stack. | Class instances are called *objects* and live on the heap. |
| Can you declare a default constructor? | No | Yes |
| If you declare your own constructor, will the compiler still generate the default constructor? | Yes | No |
| If you don’t initialize a field in your own constructor, will the compiler automatically initialize it for you? | No | Yes |
| Are you allowed to initialize instance fields at their point of declaration? | No | Yes |

There are other differences between classes and structures concerning inheritance. These differences are covered in Chapter 12, “Working with inheritance.”

# Declaring structure variables

After you have defined a structure type, you can use it in exactly the same way as you do any other type. For example, if you have defined the *Time* structure, you can create variables, fields, and parameters of type *Time*, as shown in this example:

Click here to view code image

```
struct Time
{
    private int hours, minutes, seconds;
    ...
}

class Example
{
    private Time currentTime;

    public void Method(Time parameter)
    {
        Time localVariable;
        ...
    }
}
```

# Note

As with enumerations, you can create a nullable version of a structure variable by using the ? modifier. You can then assign the *null* value to the variable:

```
Time? currentTime = null;
```