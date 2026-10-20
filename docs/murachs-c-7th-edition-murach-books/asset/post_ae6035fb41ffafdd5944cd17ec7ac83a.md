
## A method that tests an object’s type and property (C# 6.0 and earlier)

```csharp
public static decimal GetDiscountPercent(Object o) {
    decimal discountPercent = .0m;
    if (o.GetType() == typeof(Product)) {
        Product p = (Product) o;
        if (p.Category == ".NET")
            discountPercent = .1m;
        else if (p.Category == "Java")
            discountPercent = .2m;
    }
    return discountPercent;
}
```

## Methods that use pattern matching (C# 7.0 and later)

### With an if statement that tests an object’s type

```csharp
private static decimal GetDiscountPercent(Object o) {
    decimal discountPercent = .0m;
    if (o is Product p) {
        if (p.Category == ".NET")
            discountPercent = .1m;
        else if (p.Category == "Java")
            discountPercent = .2m;
    }
    return discountPercent;
}
```

### With a switch statement that tests an object’s type and property

```csharp
private static decimal GetDiscountPercent(Object o) {
    switch (o) {
        case Product p when p.Category == ".NET":
            return .1m;
        case Product p when p.Category == "Java":
            return .2m;
        default:
            return .0m;
    }
}
```

### A pattern that uses the not operator (C# 9.0 and later)

```csharp
if (o is not null) { // code to execute goes here }
```

However, it can also be used to check whether an object is not of a specific type like this:

```csharp
if (o is not Product) { // code goes here }
```

### Description

- C# 7.0 introduced *pattern matching*, which lets you use an if or switch statement to test the type of an object that’s passed to a method.
- To test the type of an object using an if statement, you use the *is operator* to code an *is expression*. This expression also assigns the object to a variable of the specified type.
- To test the type of an object using a switch statement, you code the object type and the variable you want to assign it to. You can also code a *when* clause to test if a property or field of the object has a particular value.
- With C# 9.0 and later, you can use the *not operator* in a pattern.

## How to use property patterns

In chapter 5, you learned how to use switch expressions in place of switch statements that simply return a value based on the value of an expression. Then, in chapter 6, you learned how to use switch expressions in expression-bodied methods. Now, figure 12-20 shows how to use switch expressions with a new feature of C# 8.0 called property patterns. Property patterns are an extension of the pattern matching feature that you learned about in the previous figure.

The first example in this figure shows a method like the ones you saw in the last figure that accept a generic object and return a discount percent. Instead of using an if or switch statement, though, this example uses a switch expression to test the type of object that’s passed to the method. To do that, it simply names the object type to test for on a case. For instance, the first two cases in this example test that the object is a Product object.

After the object type, you code the property pattern. This pattern includes the property name followed by a colon, the value that’s being tested for, and the enclosing braces. In this example, the property patterns test the Category property of the Product object for specific values as in the last figure. If you compare this method with the methods in the previous figure that perform the same function, you’ll see that the method that uses the property pattern is considerably simpler.

One more thing you should notice about this switch expression is that it ends with a discard. This is required when you use a switch expression with a property pattern because property patterns must return a non-null value.

The second example shows that you can use a switch expression to test for more than one type of object. Here, the first four cases test for Product objects, and the next two cases test for Vendor objects. Although you haven’t seen Vendor objects used in any of the examples up to now, all you need to know is that these objects are created from a Vendor class that includes properties, methods, and constructors similar to the ones defined by the Product class.

Notice in this example that the property patterns for the cases that test for a Vendor object test a different property than the cases that test for a Product object. You can also test different properties of the same object, and you can test two or more properties of the same object using a single property pattern as shown in the second case for a Vendor object. In other words, you can use a switch expression with property patterns to test any property of any object. That’s true regardless of whether the objects are related.

The third example in this figure is similar to the first example, except that it accepts a Product object rather than a generic object. As a result, it isn’t necessary to test the object type. However, it can only be used with Product objects.

### The syntax of a property pattern

```text
{ property: value[, property: value]... }
```

### A method that uses a switch expression with a property pattern to test an object’s type and property

```csharp
private static decimal GetDiscountPercent(Object o) => o switch
{
    Product { Category: ".NET" } => .1m,
    Product { Category: "Java" } => .2m,
    _ => .0m
};
```

### A method that tests two types of objects

```csharp
private static decimal GetDiscountPercent(Object o) => o switch
{
    Product { Category: ".NET" } => .1m,
    Product { Category: "Java" } => .2m,
    Product { Category: "Web" } => .3m,
    Product { Category: "Mainframe" } => .4m,
    Vendor { DiscountType: "Quantity" } => .2m,
    Vendor { DiscountType: "Terms", Terms: 30 } => .3m,
    _ => .0m
};
```

### A method that tests a specific type of object

```csharp
private static decimal GetDiscountPercent(Product p) => p switch
{
    { Category: ".NET" } => .1m,
    { Category: "Java" } => .2m,
    _ => .0m
};
```

### Description

- C# 8.0 introduced a new type of pattern matching called *property patterns*. You can use property patterns with switch expressions to test if a property or public field of an object has a particular value.
- A property pattern consists of the name of a property or public field, followed by a colon and the value for the pattern, all enclosed in braces. You can also use a property pattern to test the values of two or more properties or public fields by separating them with commas.
- To test the type of the object that’s passed to a method, you precede the property pattern with the name of the type.

## How to generate code stubs

In addition to the skills you just learned for creating classes, you can use a feature of Visual Studio called live code analysis to generate code stubs for a class and its members. This feature can help you quickly generate the starting code for a class from the code that uses the class. Then, you can enhance the code for the class later as needed.

Figure 12-21 shows how the Generate From Usage feature works. In the first screen shown here, you can see that I declared a variable named product from a class named Product. Because the Product class didn’t exist, though, Visual Studio marked it as a syntax error. Then, I used the first command in the Quick Actions menu for the class name to display a submenu, and I used the first command in the submenu to generate the class. The second screen is similar, but in this case, I generated a stub for a method named GetPrice().

When you point to a command in a Quick Actions menu for generating a class or member, Visual Studio displays the code that will be generated as shown here. As you can see, the code for the class consists of a namespace statement, a class statement, and a constructor. Note that the class is declared with the internal access modifier, which restricts access to the method to the current C# assembly.

The code for the method consists of the method declaration and a single statement. That statement throws an exception indicating that the method hasn’t been implemented. Then, you can replace this statement with the code that implements the method.

Like the class, this method includes the internal access modifier. In addition, because the statement that calls the GetPrice() method assigns the return value to a decimal variable, the method returns a decimal value. Finally, because the statement passes a string to the method, the method is defined with a string parameter.

In this example, the Product class is created in a new file. You can also add a class to the current file following the current class using the second command in the Quick Actions menu, and you can nest a class within the current class using the third command. You’ll learn more about nesting classes in chapter 16.

Finally, instead of automatically generating a class declaration from a statement like the one in the first example, you can use the fourth command in the Quick Actions submenu to display the Generate Type dialog box. This dialog box lets you specify the code you want to generate. For example, you can use it to specify a different access modifier for the class. Although this dialog box isn’t shown here, you shouldn’t have any trouble using it.

In most cases, you’ll use IntelliSense’s standard completion mode to enter the name of a class or member. This is the mode you’ve learned about so far in this book. When you enter the name of an undefined class or member, though, you may want to use suggestion mode instead. In this mode, the completion list is still displayed, but the current item is outlined rather than highlighted. Then, to commit the name you typed, you enter the next character in the statement or press the Enter key. This helps prevent IntelliSense from inserting unwanted text. To switch between completion mode and suggestion mode, you can use either of the two techniques described in this figure.
