
Although you can make up almost any name for a variable, most programmers adopt a standard convention for naming variables. Some common practices include the following:

- Using a mix of uppercase and lowercase characters, as in TotalCost.
- Using all lowercase characters, as in counter.
- Separating the parts of a variable's name with underscores, as in Total_Cost.
- Preceding the name with the data type of the value. A variable that stores a number (a Long Integer in this case) might be called lCounter, while a variable holding a string might be named sLastName.

The "Using a naming convention with variables" section later in this chapter goes into greater detail about the benefits of a naming convention.

> NOTE
> One source of endless confusion to Access developers is the fact that Access object names (tables, queries, forms, and so on) may contain spaces, while variable names never include spaces. One reason not to use spaces in Access object names is to eliminate confusion when mixing different naming conventions within a single application. You're really better off being consistent in how you apply names to your Access objects, variables, procedures, and other application entities.

> TIP
> When creating variables, you can use uppercase, lowercase, or both to specify the variable or call it later. VBA variables are not case sensitive. This means that you can use the TodayIs variable later without having to worry about the case that you used for the name when you created it; TODAYIS, todayis, and tOdAyIs all refer to the same variable. The VBE automatically changes any explicitly declared variables to the case that was used in the declaration statement (the Dim statement).

When you need to use the contents of a variable, you simply reference its name. When you specify the variable's name, the computer program goes into memory, finds the variable, and gets its contents for you. This process means, of course, that you need to be able to remember and correctly reference the name of the variable.

## Declaring variables

There are two principle ways to add variables to your applications. The first method—called implicit declaration—is to let VBA automatically create the variables for you. As with most things that are not carefully controlled, you'll find that letting VBA prepare your variables for you is not a particularly good idea and can lead to performance issues in, and problems debugging, your programs (see the "Comparing implicit and explicit variables" section later in this chapter).

(sFirstName and sLastName) are assigned the text contained in two text boxes (txtFirstName and txtLastName), and a third variable (sFullName) is assigned the combination of sFirstName and sLastName, with a space between them:

```
Private Sub Combine_Implicit()

    sFirstName = Me.txtFirstName.Text
    sLastName = Me.txtLastName.Text
    sFullName = sFirstName & Space(1) & sLastName

End Sub
```

The second approach is to explicitly declare them with one of the following keywords: Dim, Static, Private, or Public (or Global). The choice of keyword has a profound effect on the variable’s scope within the application and determines where the variable can be used in the program. (Variable scope is discussed in the “Understanding variable scope and lifetime” section later in this chapter.)

> **TIP**
> 
> To force explicit variable declaration, type the directive `Option Explicit` at the top of each module. Better yet, check Require Variable Declaration in the VBE Options dialog box, and all new modules will automatically include the Option Explicit directive.

The syntax for explicitly declaring a variable is quite simple:

```
Dim VariableName As DataType
Static VariableName As DataType
Private VariableName As DataType
Public VariableName As DataType
```

In each case, the name of the variable and its data type are provided as part of the declaration. VBA reserves the amount of memory required to hold the variable as soon as the declaration statement is executed. Once a variable is declared, you can’t change its data type, although you can easily convert the value of a variable and assign the converted value to another variable.

The following example shows the Combine_Implicit sub rewritten to use explicitly declared variables:

```
Private Sub Combine_Explicit()

    Dim sFirstName As String
    Dim sLastName As String
    Dim sFullName As String

    sFirstName = Me.txtFirstName.Text
    sLastName = Me.txtLastName.Text
    sFullName = sFirstName & Space(1) & sLastName

End Sub
```

So, if there’s often very little difference between using implicit and explicit variables, why bother declaring variables at all? The following code demonstrates the importance of using explicitly declared variables in your applications:

```
Private Sub Form_Load()

sDepartment = "Manufacturing"
sSupervisor = "Joe Jones"
sTitle = "Senior Engineer"

'Dozens of lines of code go here

Me.txtDepartment = sDepartment
Me.txtSupervisor = sSuperviser
Me.txtTitle = sTitle

End Sub
```

In this example code, the txtSupervisor text box on the form is always empty and is never assigned a value. A line near the bottom of this procedure assigns the value of an implicitly declared variable named Superviser to the txtSupervisor text box. Notice that the name of the variable (Superviser) is a misspelling of the intended variable (Supervisor). Because the source of the assignment appears to be a variable, VBA simply creates a new variant named Superviser and assigns its value (which is, literally, Nothing) to the txtSupervisor text box. And, because the new Superviser variable has never been assigned a value, the text box always ends up empty. Misspellings such as this are very common and easy to overlook in long or complex procedures.

Furthermore, the code shown in this example runs fine and doesn’t produce a VBA error. Because this procedure uses implicit variable declaration, Access doesn’t raise an error because of the misspelling, and the problem isn’t detected until someone notices the text box is always empty. Imagine the problems you’d encounter in a payroll or billing application if variables went missing because of simple spelling errors!

When you declare a variable, Access sets up a location in the computer’s memory for storing a value for the variable ahead of time. The amount of storage allocated for the variable depends on the data type you assign to the variable. More space is allocated for a variable that will hold a currency amount (such as $1,000,000) than for a variable that will never hold a value greater than, say, 255. This is because a variable declared with the Currency data type requires more storage than another variable declared as a Byte data type. (Data types are discussed later in this chapter, in the “Working with Data Types” section.)

Even though VBA doesn’t require you to declare your variables before using them, it does provide various declaration commands. Getting into the habit of declaring variables is good practice. A variable’s declaration assures that you can assign only a certain type of data to it—always a numeric value or only characters, for example. In addition, you attain real performance gains by pre-declaring variables.

## The Dim keyword

To declare a variable, you use the Dim keyword. (Dim is an abbreviation of the archaic Dimension programming term—because you’re specifying the dimension of the variable.) When you use the Dim keyword, you must supply the variable name that you assign to the variable. Here’s the format for a Dim statement:

```
Dim [VariableName] As [DataType]
```

The following statement declares the variable lBeeps as a Long Integer data type:

```
Dim lBeeps As Long
```

Notice that the variable name follows the Dim statement. In addition to naming the variable, use As Data Type to specify a data type for the variable. The data type is the kind of information that will be stored in the variable—String, Long, Currency, and so on. The default data type is Variant; it can hold any type of data.

Table 25.1 in the next section lists all the data types available.

When you use the Dim statement to declare a variable in a procedure, you can refer to that variable only within that procedure. Other procedures, even if they’re stored in the same module, don’t know anything about the variable declared within a procedure. Such a variable is often described as local because it’s declared locally within a procedure and is known only by the procedure that owns it. (You can read more about variable scope in the “Understanding variable scope and lifetime” section later in this chapter.)

Variables also can be declared in the declarations section of a module. Then all the procedures in the module can access the variable. Procedures outside the module in which you declared the variable, however, can’t read or use the variable.

## The Public keyword

To make a variable available to all modules in the application, use the Public keyword when you declare the variable. Figure 25.2 illustrates declaring a public variable.
