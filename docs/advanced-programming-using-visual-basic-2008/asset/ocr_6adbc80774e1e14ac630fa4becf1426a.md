# Keywords to Declare Accessibility Domains

# Table 2.1

| Keyword | Description |
|---|---|
| Public | Accessible from anywhere in the project or from any other project that references this one. |
| Private | Accessible from anywhere inside this class. |
| Protected | Accessible from anywhere inside this class or in any class that inherits from this class. |
| Friend | Accessible from anywhere inside this project/assembly. |
| Protected Friend | A combination of Protected and Friend. Accessible from anywhere inside this project/assembly and in any class that inherits from this class, even though the derived class is in a different project/assembly. |

# Creating Classes That Inherit

To create a class that inherits, you should first add a new class to the project. Although a single file can hold multiple class definitions, the recommended approach is to create a new file for each Public class and make the name of the file match the class name. The only exceptions are small "helper classes" that would never be used by any other application. These helper classes should be declared with the Friend keyword because they are used only in the current project.

# Adding a New Class File

Add a new file for a class by selecting Project / Add Class, which creates a new file with the extension .vb. Make sure to give the class the name that you want to use; the file will be named correctly and the solution and project will be set up with the correct name.

The newly added class will have the first and last lines of code:

```
Public Class ClassName
End Class
```

Add the Inherits clause on the first line following the Class declaration and add comments above the Class statement.

```
'Project: Ch02PayrollInheritance
'Module: PayrollSalaried Class
'Programmer: Bradley/Millspaugh
'Date: June 2009
'Description: A class in the business services tier for payroll calculation:
' validates input data and calculates the pay for
' salaried employees.

Public Class PayrollSalaried
    Inherits Payroll
End Class
```