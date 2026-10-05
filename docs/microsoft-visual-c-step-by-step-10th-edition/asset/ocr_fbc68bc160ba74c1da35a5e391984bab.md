> Static methods are also called class methods. However, static fields aren't usually called class fields; they're just called static fields (or sometimes static variables).

# Creating a static field by using the const keyword

By prefixing the field with the `const` keyword, you can declare that a field is static but that its value never change. The keyword `const` is short for constant. A const field doesn't use the `static` keyword in its declaration but is nevertheless static. However, for reasons that are beyond the scope of this book, you can declare a field as `const` only when the field is a numeric type (such as `int` or `double`), a string, or an enumeration. (You'll learn about enumerations in Chapter 9, "Creating value types with enumerations and structures.") For example, here's how the `Math` class declares `PI` as a `const` field:

Click here to view code image

```
class Math
{
  public const double PI = 3.1415926535897;
}
```

# Understanding static classes

Another feature of the C# language is the ability to declare a class as static. A static class can contain only static members. (All objects that you create by using the class share a single copy of these members.)

The purpose of a static class is purely to act as a holder of utility methods and fields. A static class cannot contain any instance data or methods, and it doesn't make sense to create an object from a static class using the `new` operator. In fact, you can't actually use `new` to create an instance of an object using a static class even if you want to. (The compiler will report an error if you try.) If you need to perform any initialization, a static class can have a default constructor as long as it is also declared as static. Any other types of constructor are illegal and will be reported as such by the compiler.