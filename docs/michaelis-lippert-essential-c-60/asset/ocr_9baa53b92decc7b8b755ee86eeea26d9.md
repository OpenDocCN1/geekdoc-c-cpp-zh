# BEGINNER TOPIC

# Categories of Types

All types discussed so far have fallen into one of two categories: reference types and value types. The differences between the types in each category stem from differences in copying strategies, which in turn result in each type being stored differently in memory. As a review, this Beginner Topic reintroduces the value type/reference type discussion for those readers who are unfamiliar with these issues.

# Value Types

Variables of **value types** directly contain their values, as shown in Figure 8.1. The variable name is associated directly with the storage location in memory where the value is stored. Because of this, when a second variable is assigned the value of an original variable, a copy of the original variable’s value is made to the storage location associated with the second variable. Two variables never refer to the same storage location (unless one or both are out or ref parameters, which are, by definition, aliases for another variable). Changing the value of the original variable will not affect the value in the second variable, because each variable is associated with a different storage location. Consequently, changing the value of one value type variable cannot affect the value of any other value type variable.

![](bbox=[0.132, 0.611, 0.535, 0.745])

```
```csharp
//...
int number1 = 42;
char letter = 'A';
float pi = 3.14F;
int number2 = number1;
//...
```
```

A value type variable is like a piece of paper that has a number written on it. If you want to change the number, you can erase it and replace it with a different number. If you have a second piece of paper, you can copy the number from the first piece of paper, but the two pieces of paper are then