reference type or object such as the formula “expression is type,” which is also equivalent to a single call to “expression is type? (type) expression: (type) null” (see Example 5.46).

> The null reference refers to an object that has not yet been assigned; it basically serves as a blank or nonvalue, which can be substituted for later. It is also the default value to any nonassigned reference types, and can be used to mark a position where no actual reference is needed.

# Example 5.46. The binary operator as.

```
using System;
namespace Chapter5 {
    public class TestAS {
        public static void Main() {
            object MyString = new object();
            MyString = 123;

            string s = MyString as string;

            if (s != null)
                Console.WriteLine(MyString);
            else
                Console.WriteLine("Test Failed!");
        }
    }
}
```

# Delegates

Delegates are objects used as references to encapsulate specific methods, which include signatures and formal return types. The delegate, while similar to the C++ function pointer, is actually type safe and considered OOP (Object-Oriented Programming) compliant. Delegates also allow for six key modifiers: new, public, protected, internal, private, and unsafe (unsafe is only used when dealing with parameters that are also pointers). Delegates are most frequently used to pass methods as parameters. Type safety is based on the matching of signatures as part of their declaration—delegates need to be declared before they are called (see Example 5.47).