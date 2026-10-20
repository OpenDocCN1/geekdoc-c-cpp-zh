
## How to code expression-bodied methods and constructors

In chapter 6, you learned the basic skills for coding *expression-bodied methods*. Now, figure 12-18 shows how to code expression-bodied methods in the classes you create. Like expression-bodied properties, expression-bodied methods were introduced with C# 6.0.

As you learned in chapter 6, an expression-bodied method can return the value of an expression or execute a single statement. For instance, the first example in this figure shows one version of the GetDisplayText() method that you saw earlier in this chapter. This method returns a string with the values of three instance variables separated by the string that’s passed to the sep parameter.

The statement that follows shows how to code this method using an expression body. To do that, you code the method signature just like you do for any other method, followed by the lambda operator and the expression to be returned.

The second example shows a method that displays the values of three instance variables in a dialog box. The method with the expression body differs from the method in the first example in two ways. First, the expression body consists of an executable statement instead of an expression. Second, the return type is void since the method doesn’t return a value.

Unlike expression-bodied properties, expression-bodied methods don’t provide for much simplification of code. Even so, you should consider using them for consistency when you use the lambda operator for other purposes in your code. In chapter 5, for example, you learned how to use the lambda operator with switch expressions, and in chapter 13, you’ll learn how to use the lambda operator to code expression-bodied indexers and operators as well as lambda expressions, which are frequently used with LINQ as shown in chapter 20.

You can also use expression bodies with constructors, starting with C# 7.0. This is illustrated by the third example in this figure. Here, the constructor consists of a single statement that initializes an instance variable.

The statement that follows shows how to code this constructor as an *expression-bodied constructor*. To do that, you code the signature for the constructor, followed by the lambda operator and the statement to be executed.

You can also use an expression-bodied constructor with a constructor that initializes two or more instance variables. This is illustrated by the last example. Here, the constructor initializes the values of three instance variables.

To code this constructor using an expression body, you use a tuple like the ones you learned about in chapter 6. In this case, a tuple is created from the three parameters that are passed to the constructor. Then, the tuple is deconstructed and its values are assigned to the corresponding instance variables. Notice here that it isn’t necessary to declare types for the tuple members. That’s because the types are already declared in the parameter list for the constructor.

Note that, just as you can for properties and accessors, you can use refactoring to convert methods and constructors that use block bodies to expression-bodied methods and constructors. Note, however, that this doesn’t work for constructors that initialize two or more instance variables.

### A method that returns the value of an expression

```csharp
public string GetDisplayText(string sep) {
    return code + sep + price.ToString("c") + sep + description;
}
```

### The same method using an expression body

```csharp
public string GetDisplayText(string sep) =>
    code + sep + price.ToString("c") + sep + description;
```

### A method that executes a single statement

```csharp
public void DisplayProduct() {
    MessageBox.Show("Code: " + code + "\n" +
        "Price: " + price.ToString("c") + "\n" +
        "Description: " + description, "Product");
}
```

### The same method using an expression body

```csharp
public void DisplayProduct() =>
    MessageBox.Show("Code: " + code + "\n" +
        "Price: " + price.ToString("c") + "\n" +
        "Description: " + description, "Product");
```

### A constructor with one parameter

```csharp
public Product(string code) {
    this.Code = code;    // set other properties to default values
}
```

### The same constructor using an expression body

```csharp
public Product(string code) => this.Code = code;
```

### A constructor with three parameters

```csharp
public Product(string code, string description, decimal price) {
    this.Code = code;
    this.Description = description;
    this.Price = price;
}
```

### The same constructor using an expression body with a tuple

```csharp
public Product(string code, string description, decimal price) =>
    (this.Code, this.Description, this.Price) = (code, description, price);
```

### Description

- If a method simply returns an expression or executes a single statement, you can code it as an *expression-bodied method*.
- To code an expression-bodied method, you code the method signature, followed by the lambda operator (=>) and an expression or executable statement.
- If a constructor contains a single statement, you can code it as an *expression-bodied constructor* using the lambda operator.
- If a constructor contains two or more statements that initialize instance variables, you can use an expression-bodied constructor with a tuple to initialize those variables.
- Expression-bodied methods were introduced with C# 6.0, while expression-bodied constructors were introduced with C# 7.0.

## How to use pattern matching

In some cases, you’ll need to code methods that test if an object has a particular type. To do that with C# 6.0 and earlier, you had to use the GetType() method and the typeof operator as shown in the first example in figure 12-19. This example shows a method named GetDiscountPercent() that accepts a generic object and returns a discount percent based on the type of that object.

For the GetDiscountPercent() method to work, it must test if the object that’s passed to it is a Product object. To do that, it calls the GetType() method, which returns a Type object that represents an object’s type. Then, it uses the typeof operator to get a Type object for the Product class. If these two Type objects are equal, it means that a Product object was passed to the method.

If a Product object is passed to the method, the method casts the object to a Product object. Then, it uses an if-else statement to test the value of the Category property of the product and set the discount percent based on that value.

Although this example tests for a single object type, you should know that it could be expanded to test for additional types. To do that, you would add else if clauses to the outer if statement. In fact, you typically define a method parameter with the Object type so the method can work with any type of object. We present just one object type here for simplicity.

To simplify the way you test for object types, C# 7.0 introduced a feature called pattern matching. To use pattern matching with an if statement, you use the is operator as illustrated by the second GetDiscountPercent() method. Here, the is operator is used to test that the object that’s passed to the method is a Product object. As you can see, this simplifies the conditional expression for the if statement. In addition, if the object is a Product object, the is operator assigns the object to a variable of the Product type. In this case, that’s a variable named p. Because of that, it isn’t necessary to code a separate statement to do that.

You can also use pattern matching with switch statements, as shown in the third GetDiscountPercent() method. To test for a type with a switch statement, you simply code that type on a case label, along with the name of a variable where the object will be stored if it’s that type. In this example, both case labels test for a Product object and store that object in a variable named p. Notice that these case labels don’t include break statements. That’s because the return statements return control immediately to the calling code.

In addition to testing for an object type, you can use a when clause on each case label to test the value of a property or public field. In this example, both case labels test the value of the Category property of the Product object just as in the first two examples.

Like the first method, the two methods that use pattern matching can test for different types of objects. When you use pattern matching with an if statement, for example, you can add else if clauses to the outer if statement that use the is operator to test for different object types. And when you use pattern matching with a switch statement, you can code additional case labels that test for different object types.

With C# 9.0 and later, you can use the not operator in a pattern. This is useful for checking whether an object is not null as shown by the fourth example.
