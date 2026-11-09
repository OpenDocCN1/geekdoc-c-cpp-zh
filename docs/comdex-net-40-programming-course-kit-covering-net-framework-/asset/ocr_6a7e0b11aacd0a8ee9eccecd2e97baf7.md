property. The get accessor is used to retrieve the value of the variable represented by a property and the set accessor is used to assign a new value to that variable.

The following code snippet shows how to add a property to a class:

```
class Class1
{
    private string empName;
    public string MyProperty
    {
        get
        {
            return empName;
        }
        set
        {
            empName = value;
        }
    }
}
```

In the preceding code snippet, empName is the name of the variable and the MyProperty is the name of the property. The Myproperty property contains get and set accessor functions, which are used for assigning a value to the empName variable, and return the value when needed.

# Class Objects

The members of a class cannot be directly accessed from outside the class. To access the members of a class outside the class, you need to create an object of the class. All objects of a class have their own copies of the members of the class. For example, if you create two objects, named c1 and c2, of the class, Count, then both objects can access the variables and methods of this class separately by using their own copy of variables.

The syntax to create an object in C# is as follows:

```
<class-name> <object-name> = new <class-name>();
```

In the preceding syntax, object-name represents the name of the object that you want to create and class-name represents the class for which you create an object. After creating an object of a class, you can access members of that class through the object. The syntax to access the members of a class through the class object is as follows:

```
object-name.variable-name;
object-name.method-name();
```

In the preceding syntax, object-name refers to the object of the class. The dot operator (.) is used to access the members of the class; whereas, the variable-name and method-name are the names of the variable and method that you want to access.

Perform the following steps to access the members of a class by creating an object of the class:

+   1. *Start* Visual Studio 2010.
+   2. *Select* File➔New➔Project from the menu bar. The New Project dialog box opens.
+   3. *Select* Visual C#➔Windows from the Installed Templates section in the left pane of the New Project dialog box. The project templates available for developing Windows applications in Visual C# are displayed in the right pane of the New Project dialog box.
+   4. *Select* Console Application from the right pane to create a Console application.
+   5. *Enter* the name of the application as CreatingObjects (also available on the CD) in the Name text box and an appropriate location for the application in the Location box.
+   6. *Click* the OK button to close the New Project dialog box and create the CreatingObjects application.
+   7. *Add* the highlighted code snippet, shown in Listing 2.1, to the Program.cs file: