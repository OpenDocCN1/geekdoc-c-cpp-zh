# A method that returns the value of an expression

```
public string GetDisplayText(string sep) {
    return code + sep + price.ToString("c") + sep + description;
}
```

# The same method using an expression body

```
public string GetDisplayText(string sep) =>
    code + sep + price.ToString("c") + sep + description;
```

# A method that executes a single statement

```
public void DisplayProduct() {
    MessageBox.Show("Code: " + code + "\n" +
        "Price: " + price.ToString("c") + "\n"
        "Description: " + description, "Product");
}
```

# The same method using an expression body

```
public void DisplayProduct() =>
    MessageBox.Show("Code: " + code + "\n" +
        "Price: " + price.ToString("c") + "\n" +
        "Description: " + description, "Product");
```

# A constructor with one parameter

```
public Product(string code) {
    this.Code = code;    // set other properties to default values
}
```

# The same constructor using an expression body

```
public Product(string code) => this.Code = code;
```

# A constructor with three parameters

```
public Product(string code, string description, decimal price) {
    this.Code = code;
    this.Description = description;
    this.Price = price;
}
```

# The same constructor using an expression body with a tuple

```
public Product(string code, string description, decimal price) =>
    (this.Code, this.Description, this.Price) = (code, description, price);
```

# Description

+   - If a method simply returns an expression or executes a single statement, you can code it as an *expression-bodied method*.
+   - To code an expression-bodied method, you code the method signature, followed by the lambda operator (=>) and an expression or executable statement.
+   - If a constructor contains a single statement, you can code it as an *expression-bodied constructor* using the lambda operator.
+   - If a constructor contains two or more statements that initialize instance variables, you can use an expression-bodied constructor with a tuple to initialize those variables.
+   - Expression-bodied methods were introduced with C# 6.0, while expression-bodied constructors were introduced with C# 7.0.