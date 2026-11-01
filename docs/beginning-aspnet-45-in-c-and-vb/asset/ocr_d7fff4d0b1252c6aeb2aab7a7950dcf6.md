The first thing you'll notice is that C# uses a double equals symbol (==) for the standard comparison operator. This clearly makes it different from the assignment operator. It's a common mistake in C# to use only a single equals symbol if you intend to compare two values. Consider the following example:

```
if (result = 4)
{
    // Do something here with result
}
```

The intention here is to see if result equals 4. However, because the assignment operator is used instead of a proper comparison operator, you'll get the compile error that is displayed in Figure 5-2.

![](bbox=[0.18, 0.48, 0.58, 0.58])

# FIGURE 5-2

At first the error message may look a little strange. But if you look at the code a little closer, it starts to make more sense. First, result gets assigned a value of 4. This value is then used for the if statement. However, the if statement needs a boolean value to determine whether it should run the code inside the if block. Because you can't convert an integer value to a boolean like this, you get a compile error. The fix is easy, though; just use the proper comparison operator instead:

```
if (result == 4)
{
    // Do something here with result
}
```

Similar to the simple comparison operator, you can use the other operators to compare values:

# VB.NET

```
4 > 5    ' 4 is not greater than 5; evaluates to False
4 <> 5   ' 4 is not equal to 5; evaluates to True
5 >= 4   ' 5 is greater than or equal to 4; evaluates to True
```

# C#

```
4 > 5    // 4 is not greater than 5; evaluates to false
4 != 5   // 4 is not equal to 5; evaluates to true
5 >= 4   // 5 is greater than or equal to 4; evaluates to true
```

The Is keyword in VB.NET and is in C# do something completely different. In VB.NET, Is compares two instances of objects, something you learn more about in the second half of this chapter. In C#, you use is to find out if a certain variable is compatible with a certain type. You can accomplish that in VB.NET using the TypeOf operator. The following two examples are functionally equivalent:

# VB.NET

```
Dim myTextBox As TextBox = New TextBox()

If TypeOf myTextBox Is TextBox Then
```