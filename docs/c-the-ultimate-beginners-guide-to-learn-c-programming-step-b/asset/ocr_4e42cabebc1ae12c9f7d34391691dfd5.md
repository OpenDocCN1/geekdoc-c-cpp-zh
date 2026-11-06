+   - The initializer cannot be null and must be an expression.
+   - Multiple, implicitly typed variables cannot be initialized in the same statement.
+   - An object cannot be initialized unless a new object is created in the initializer.

# **Default Value Expressions**

Default value expressions are especially useful in combination with generic types when you don’t know in advance what the default value for the given type will be.

default(T) Expression: Old Way

A default value expression **default(T)** returns the default value of a type T, where T is a reference type or a value type.

```
T variableName = default(T); // syntax
```

# **Example:**

```
var name = default(string); var age = default(int); var weight = default(int); var isMarried = default(bool);
```

default literal: New Way

The **default literal** is a new feature in C# 7.1 that is used to get the default value of the specified data type when the statement is executed. This feature works for value types as well as reference types.

**Note:** default literal is equivalent to default(T) where T is the inferred type.

```
string name = default; int age = default; int weight = default; bool isMarried = default;
Console.WriteLine(name); Console.WriteLine(age);
Console.WriteLine(weight); Console.WriteLine(isMarried);
```

In the output below, a null value is printed as a blank line.

OUTPUT for default literal & default(T):

```
0 0 False
```

new Operator:

Using the **new** operator invokes the default constructor of a value type. This allows you to create a variable using the **new** keyword, which automatically sets the variable to its default value.

**Note:** All values in C# are an instance of a specific type.