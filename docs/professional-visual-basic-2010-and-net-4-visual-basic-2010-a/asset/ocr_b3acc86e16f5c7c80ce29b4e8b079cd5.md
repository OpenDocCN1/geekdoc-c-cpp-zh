The Class View window is extremely useful even if you stick with one class per file, because it still provides you with a class-based view of the entire application.

This chapter uses one class per file in the examples, as this is the most common approach. To begin, open the Visual Studio IDE and create a new Windows Forms Application project named “ObjectIntro.” Choose the Project ➕ Add Class menu option to add a new class module to the project. You’ll be presented with the standard Add New Item dialog. Change the name to Person.vb and click Add. The result will be the following code, which defines the Person class:

```
Public Class Person

End Class
```

With the Person class created, you are ready to start adding code to declare the interface, implement the behaviors, and declare the instance variables.

# Fields

Fields are variables declared in the class. They will be available to each individual object when the application is run. Each object gets its own set of data — basically, each object gets its own copy of the fields.

Earlier, you learned that a class is simply a template from which you create specific objects. Variables that you define within the class are also simply templates — and each object gets its own copy of those variables in which to store its data.

Declaring member variables is as easy as declaring variables within the Class block structure. Add the following code to the Person class:

```
Public Class Person

    Private mName As String
    Private mBirthDate As Date
End Class
```

You can control the scope of the fields with the following keywords:

+   - Private — Available only to code within the class
+   - Friend — Available only to code within the project/component
+   - Protected — Available only to classes that inherit from the class (discussed in detail in Chapter 3)
+   - Protected Friend — Available to code within your project/component and classes that inherit from the class whether in the project or not (discussed in detail in Chapter 3)
+   - Public — Available to code outside the class and to any projects that reference the assembly

Typically, fields are declared using the Private keyword, making them available only to code within each instance of the class. Choosing any other option should be done with great care, because all the other options allow code outside the class to directly interact with the variable, meaning that the value could be changed and your code would never know that a change took place.

> One common exception to making fields Private is to use the Protected keyword, discussed in Chapter 3.

# Methods

Objects typically need to provide services (or functions) that can be called when working with the object. Using their own data or data passed as parameters to the method, they manipulate information to yield a result or perform an action.

Methods declared as Public, Friend, or Protected in scope define the interface of the class. Methods that are Private in scope are available to the code only within the class itself, and can be used to provide