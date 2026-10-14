a box in the computer’s memory that holds temporary information. You must give each variable in a program an unambiguous name that uniquely identifies it in the context in which it is used. You use a variable’s name to refer to the value it holds. For example, if you want to store the value of the cost of an item in a store, you might create a variable simply called cost and store the item’s cost in this variable. Later on, if you refer to the cost variable, the value retrieved will be the item’s cost that you stored there earlier.

# Naming variables

You should adopt a naming convention for variables that helps you avoid confusion concerning the variables you have defined. This is especially important if you are part of a project team with several developers working on different parts of an application; a consistent naming convention helps to avoid confusion and can reduce the scope for bugs. The following list contains some general recommendations:

+   - Don’t start an identifier with an underscore. Although this is legal in C#, it can limit the interoperability of your code with applications built by using other languages, such as Microsoft Visual Basic.
+   - Don’t create identifiers that differ only by case. For example, do not create one variable named myVariable and another named MyVariable for use at the same time because it is too easy to confuse one with the other. Also, defining identifiers that differ only by case can limit the ability to reuse classes in applications developed with other languages that are not case sensitive, such as Visual Basic.
+   - Start the name with a lowercase letter.
+   - In a multiword identifier, start the second and each subsequent word with an uppercase letter. (This is called camelCase notation.)
+   - Don’t use Hungarian notation. (If you are a Microsoft Visual C++ developer, you are probably familiar with Hungarian notation. If you don’t know what Hungarian notation is, don’t worry about it!)

For example, score, footballTeam, _score, and FootballTeam are all valid variable names, but only the first two are recommended.

# Declaring variables

Variables hold values. C# has many different types of values that it can store and process—integers, floating-point numbers, and strings of characters, to name three. When you declare a variable, you must specify the type of data it will hold.

You declare the type and name of a variable in a declaration statement. For example, the statement that follows declares that the variable named age holds int (integer) values. As always, you must terminate the statement with a semicolon.