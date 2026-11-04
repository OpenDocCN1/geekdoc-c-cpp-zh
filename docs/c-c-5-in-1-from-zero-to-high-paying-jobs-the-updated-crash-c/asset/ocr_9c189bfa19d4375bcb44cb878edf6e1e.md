```
void divide(int numerator, int denominator) {
    if (denominator == 0) {
        throw std::runtime_error("Division by zero");
    }
    // Perform division
}
```

# Catching Exceptions:

The `catch` blocks are evaluated in the order they appear. The first matching `catch` block is executed. If no matching `catch` block is found, the program terminates.

```
try {
    divide(10, 0);
}
catch (const std::runtime_error& ex) {
    std::cerr << "Error: " << ex.what() << std::endl;
}
```

# Creating Custom Exception Classes:

# Defining Custom Exceptions:

You may define your own exception classes by inheriting from the standard `std::exception` class or its derived classes. This allows you to create specific exception types that capture unique error scenarios.