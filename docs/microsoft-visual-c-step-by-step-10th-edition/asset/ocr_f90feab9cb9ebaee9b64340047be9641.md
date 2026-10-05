# Using variables

A variable is a storage location that holds a value. You can think of a variable as a box in the computer's memory that holds temporary information. You must give each variable in a program an unambiguous name that uniquely identifies it in the context in which it is used.

You use a variable's name to refer to the value it holds. For example, if you want to store the value of the cost of an item in a store, you might create a variable called cost and store the item's cost in this variable. Later, if you refer to the cost variable, the value retrieved will be the item's cost that you stored earlier.

# Naming variables

You should adopt a naming convention for variables to help avoid confusion concerning the variables you have defined. This is especially important if you are part of a project team with several developers working on different parts of an application. A consistent naming convention helps to avoid confusion and reduce the scope for bugs. The following list contains some general naming recommendations:

+   - Don't start an identifier with an underscore. Although this is legal in C#, it can limit the interoperability of your code with applications built by other languages, such as Microsoft Visual Basic.

+   - Don't create identifiers that differ only by case. For example, don't create one variable named myFunction and another named MyVariable for the same time because it's too easy to confuse one with the other. Also, defining identifiers that differ only by case can limit the ability to reuse classes in applications developed with other languages that are not case sensitive, as Visual Basic.

+   - Start the name with a lowercase letter.

+   - In a multi-word identifier, start the second and subsequent word with an uppercase letter. (This is called camelCase notation.)

+   - Don't use Hungarian notation. (If you are a Microsoft Visual C++ developer, you're probably familiar with Hungarian notation. If you don't know what Hungarian notation is, don't worry about it!)