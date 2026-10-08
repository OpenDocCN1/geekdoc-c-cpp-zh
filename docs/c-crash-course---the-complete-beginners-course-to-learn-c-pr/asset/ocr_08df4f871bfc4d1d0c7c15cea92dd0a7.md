```
public string first_name;
public string last_name;
public string phone;
}
```

In the above snippet, we added some more code to the class constructor. First, we added a parameter to our constructor. The only way you can instantiate the class now is if you pass a first name to the constructor. You could pass an empty string to the parameter, but you must pass something to it.

The code within the constructor sets the local property to the variable value passed to the constructor. In this example, the first name is passed to the constructor and then the value is assigned to the local variable. You know that the local variable is used because of the "this" notation. The "this" specifier means that you want to use a local variable within the class.

You can have multiple constructors within a class. You could give your users the option to use a constructor that doesn't require a parameter along with the one that requires a first name. The following code illustrates how you can do this.

```
public class Customer
{
    public Customer()
    {
        // do nothing
    }
    public Customer (string first_name)
    {
        this.first_name = first_name;
    }
    public string first_name;
    public string last_name;
    public string phone;
}
```

In the above class code, you now have the option to instantiate with no parameters or with the constructor that automatically assigns the first name to the class property. If you already have the user's first name in your code, using this constructor would be a shortcut.

# Creating Methods in Your Code

Methods are the actions that your classes perform on the program's data. Methods are basically functions within your classes. They are also called the "verbs" of your