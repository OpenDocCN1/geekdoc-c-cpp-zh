# 12.19 CONSTANT MEMBERS

C# permits declaration of data fields of a class as constants. This can be done using the modifier const. Example:

```
public const int size = 100;
```

The member size is assigned the value 100 at compile time and cannot be changed later. Any attempt to assign a value to it will result in compilation error. It also means its value must be set when it is defined. For instance:

```
public const int size;
```

is wrong and will cause a compilation error. The const members are implicitly static. The value is by definition constant and therefore only one copy of it is stored which is common for all objects of the class. This implies that we must access the const members using the class name as we do with the static members.

Although const members are implicitly static, we cannot declare them so explicitly using static. For example, the statement

```
public static const int size = 100;
```

is wrong and will produce compile-time error.

# 12.20 READONLY MEMBERS

There are situations where we would like to decide the value of a constant member at run-time. We may also like to have different constant values for different objects of the class. To overcome these shortcomings, C# provides another modifier known as readonly to be used with data members. This modifier is designed to set the value of the member using a constructor method, but cannot be modified later. The readonly members may be declared as either static fields or instance fields. When they are declared as instance fields, they can take different values with different objects. Consider the code below: