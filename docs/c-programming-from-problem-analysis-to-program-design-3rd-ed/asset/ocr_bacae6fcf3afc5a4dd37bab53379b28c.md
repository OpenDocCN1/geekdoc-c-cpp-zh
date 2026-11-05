# Return Type

The return type identifies what type of value is returned when the method is completed. Any of the predefined or valid user-defined types can be returned. Methods can return a value when all the statements of the method are complete, or they can simply return control to the method that called them, without bringing a value back.

The return type is always listed immediately preceding the name of the method, as shown in Figure 3-1. Methods do not have to return anything; however, they can return at most one data type through the method's name.

> You will learn about arrays and collections such as ArrayLists in Chapter 7. C# allows a method to return a collection; however, the return must be through a single identifier. That identifier can be the name of an array.

If a method does not return a value, the void keyword is placed at the return type location in the method heading, as shown in the following line of code:

```
public void DisplayInstructions( )
```

If a return type other than void is specified in the method heading, there must be a return statement included in the body of the method. The value returned must be a compatible value—one that either matches the type in the heading or can be stored in that type.

The return statement takes the form:

```
return [value];
```

Note that value is enclosed in square brackets to indicate that it is optional. If the method heading uses void as the return type, the return statement can be omitted or included as follows:

```
return;
```

Whenever the return type is not void, you must have a return value following the return keyword. This value can be a literal, arithmetic expression, or variable that holds a value. Example 3-3 illustrates returning a calculated value.

# Example 3-3

```
public static double CalculateMilesPerGallon
    (int milesTraveled, double gallonsUsed)
{
    return milesTraveled / gallonsUsed;
}
```