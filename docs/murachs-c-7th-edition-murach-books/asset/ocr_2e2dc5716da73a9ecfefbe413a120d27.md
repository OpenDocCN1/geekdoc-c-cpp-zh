# The syntax for coding an auto-implemented property

```
public type PropertyName { get; [set;] } [= value]
```

# An auto-implemented property with both get and set accessors

```
public string Code { get; set; }
```

# An auto-implemented property with a get accessor and an initial value

```
public string Code { get; } = "C#";
```

# A statement that sets the value of an auto-implemented property

```
product.Code = txtProductCode.Text;
```

# A statement that gets the value of an auto-implemented property

```
string code = product.Code;
```

# An auto-implemented property with an init-only setter (C# 9.0 and later)

```
public string Code { get; init; };
```

# A statement that uses an object-initializer to set the init-only property

```
var product2 = new Product { Code = "C#" };
```

# Description

+   - If the get accessor for a property simply returns the value of its instance variable and the set accessor simply assigns a value to its instance variable, you can create an *auto-implemented property*. Auto-implemented properties were introduced with C# 6.0.
+   - When you create an auto-implemented property, a corresponding private instance variable is created automatically, and that variable is only accessible through the property.
+   - An auto-implemented property can consist of both the get and set keywords or just a get keyword.
+   - You can initialize the value of the private instance variable for an auto-implemented property by coding an equals sign and the value following the closing brace for the property.
+   - You can use refactoring to convert a standard property to an auto-implemented property.
+   - With C# 9.0 and later, you can use the init keyword instead of the set keyword to create an init-only setter. Then, you can only set the value of the property when the object is being initialized by a constructor or by an object initializer as described in figure 12-4.