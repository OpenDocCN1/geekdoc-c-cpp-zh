# A class that contains static members

```
public static class Validator {
    private static string title = "Entry Error";

    public static string Title {
        get {
            return title;
        }
        set {
            title = value;
        }
    }

    public static bool IsPresent(TextBox textBox) {
        if (textBox.Text == "") {
            MessageBox.Show(textBox.Tag + " is a required field.", Title);
            textBox.Focus();
            return false;
        }
        return true;
    }
}
```

# Code that uses static members

if ( Validator.IsPresent(txtCode) &&
    Validator.IsPresent(txtDescription) &&
    Validator.IsPresent(txtPrice) )
    isValidData = true;
else
    isValidData = false;

# Description

+   - A static member is a field, property, or method that can be accessed without creating an instance of the class. To define a static member, you use the static keyword.
- Static properties and methods can refer only to other static members or to variables declared within the property or method.
- A constant that's declared with the public keyword is implicitly static. You cannot code the static keyword on a constant declaration.
- If you create an object from a class, you can refer to a static member only through the name of the class.
- If a class only contains static members, you can use the static keyword in the declaration to declare the class as a static class. This prevents programmers from accidentally adding a non-static member to the class or from creating an object from the class.

Figure 12-10 How to code static members