
# Part VI: Microsoft Access Programming Fundamentals

## FIGURE 24.17

The Project Properties dialog box contains a number of interesting options.

![](img/1e45673ab6eca9d20e67635ff5b9b318_841_0.png)

## Project Name

Certain changes in an application’s structure require Access to recompile the code in the application. For example, changing the code in a standard module affects all statements in other modules using that code, so Access must recompile all the code in the application. Until the code is recompiled, Access “decompiles” the application by reverting to the plain-text version of the code stored in the ACCDB file and ignoring the compiled code in the ACCDB. This means that each line of the code must be interpreted at run time, dramatically slowing the application.

Sometimes insignificant modifications, such as changing the name of the project itself, are sufficient to cause decompilation. This happens because of the hierarchical nature of Access VBA. Because all objects are “owned” by some other object, changing the name of a high-level object might change the dependencies and ownerships of all objects below it in the object hierarchy.

Access maintains a separate, independent project name for the code and executable objects in the application. Simply changing the name of the ACCDB file is not enough to decompile the code in an Access application. By default, the project name is the same as the name of the ACCDB, but it’s not dependent on it. You can assign a unique name to the project with the Project Name text box in the General tab of the Project Properties dialog box.

## Project Description

The Project Description is, as its name implies, a description for the project. Because this area is so small, it isn't possible to add anything of significance that might be helpful to another developer.

## Conditional Compilation Arguments

Compiler directives instruct the Access VBA compiler to include or exclude portions of code, depending on the value of a constant established in the module's declarations section. Code lines that begin with # are conditionally compiled.

One of the limitations of using compiler directives is that the constant declaration is local to the module. This means that you have to use the #Const compiler directive to set up the constant in every module that includes the #If directive. This limitation can make it difficult to remove all the #Const compiler directives to modify the code at the conclusion of development.

For example, consider a situation in which you want to use conditional compilation to include certain debugging statements and functions during the development cycle. Just before shipping the application to its users, you want to remove the compiler directives from the code so that your users won't see the message boxes, status bar messages, and other debugging information. If your application consists of dozens of forms and modules, you have to make sure you find every single instance of the #Const directive to make sure you successfully deactivated the debugging code. (This is why it's such a good idea to apply a naming convention to the identifiers you use with the #Const directive.)

Fortunately, Access provides a way for you to set up "global" conditional compilation arguments. The General tab of the Project Properties dialog box contains the Conditional Compilation Arguments text box, where you can enter arguments to be evaluated by the conditional compilation directives in your code.

As an example, assume you've set up the following sort of statements in all the modules in your application:

```
#If CC_DEBUG2 Then
MsgBox "Now in ProcessRecords()"
#End If
```

Instead of adding the constant directive (#Const CC_DEBUG2 = True) to every module in the application, you might enter the following text into the Conditional Compilation Arguments text box:

```
CC_DEBUG2 = -1
```

This directive sets the value of CC_DEBUG2 to -1 (True) for all modules (global and form and report class modules) in the application. You need to change only this one entry to CC_DEBUG2=0 to disable the debugging statements in all modules in the application.

> NOTE
> You don’t use the words true or false when setting compiler constants in the Project Properties dialog box, even though you do use these values within a VBA code module. You must use −1 for true and 0 for false in the Project Properties dialog box.

Separate multiple arguments with colons—for example: CC_DEBUG1=0 : CC_DEBUG2=−1.

## Project protection

The Protection tab contains a Lock Project for Viewing check box that, when checked, asks for a password when you (or someone else) tries to open the module. You must supply a password (and confirm it) when using this option. Don’t forget your password, because there’s no official way to get it back.

## Mastering VBA Data Types and Procedures

### IN THIS CHAPTER

- Naming and declaring variables
- Looking at the VBA data types
- Understanding the scope and lifetime of variables
- Using constants
- Looking at arrays
- Working with subs and functions
- Building functions

All VBA applications require variables to hold data while the program executes. Variables are like a white board where important information can be temporarily written and read later on by the program. For example, when a user inputs a value on a form, you may need to use a variable to temporarily hold the value until it can be permanently stored in the database or printed on a report. Simply put, a variable is the name you’ve assigned to a particular bit of data in your application. In more technical terms, a variable is a named area in memory used to store values during program execution.

Variables are transient and do not persist after an application stops running. And, as you’ll read in the “Understanding variable scope and lifetime” section later in this chapter, a variable may last a very short time as the program executes or may exist as long as the application is running.

In most cases, you assign a specific data type to each of the variables in your applications. For example, you may create a string variable to hold text data such as names or descriptions. A currency variable, on the other hand, is meant to contain values representing monetary amounts. You shouldn’t try to assign a text value to a currency variable because a runtime error may occur as a result.

The variables you use have a dramatic effect on your applications. You have many options when it comes to establishing and using variables in your Access programs. Inappropriately using a variable can slow an application’s execution or potentially cause data loss.

This chapter contains everything you need to know about creating and using VBA variables. The information in this chapter helps you use the most efficient and effective data types for your variables while avoiding the most common problems related to VBA variables.

## Using Variables

One of the most powerful concepts in programming is the variable. A variable is a temporary storage location for some value and is given a name. You can use a variable to store the result of a calculation, hold a value entered by the user, or read from a table, or you can create a variable to make a control's value available to another procedure.

To refer to the result of an expression, you use a variable's name to store the result. To assign an expression's result to a variable, you use the = operator. Here are some examples of expressions that assign values to variables:

```
counter = 1

counter = counter + 1

today = Date()
```

## FIGURE 25.1

Variable declarations appear at the top of VBA procedures.

![](img/1e45673ab6eca9d20e67635ff5b9b318_845_0.png)

- The Dim keyword establishes the new variables—sFormName and sCriteria—within a procedure.
- You provide a meaningful name for the variable as part of the Dim statement. In Figure 25.1, the variable names are sFormName and sCriteria, indicating how the variables are used by the procedure.
- The Dim statement includes the data type of the new variable. In Figure 25.1, both variables are declared as the String data type.
- Different techniques can be used to assign a value to a variable. Figure 25.1 uses the = operator to assign a literal value—frmContactLog—to sFormName. Notice that frmContactLog is surrounded by quotation marks, making it a literal value. A value pulled from the txtContactID text box on the form is combined with a literal string—" [ContactID] ="—and assigned to the sCriteria variable. The data assigned to variables should always be appropriate for the variable's data type.
- Variables are manipulated with a variety of operators. Figure 25.1 uses the VBA concatenation operator (&) to combine [ContactID] = and the value in txtContactID.

There are a number of ways to perform each of the tasks you see in Figure 25.1. For example, as you'll read in the "Declaring variables" section later in this chapter, the Dim statement is not the only way to establish a variable. And, as you'll see throughout this book, the = operator is not the only way to assign a value to a variable. Also, you don't need to use a variable like sCriteria to temporarily hold the value generated by combining two values. The two values can just as easily be combined on the fly within the DoCmd.OpenForm statement:

```
DoCmd.OpenForm "frmContactLog", _
    "[ContactID] = " & Me![txtContactID]
```

Very few rules govern how you declare and use your variables. You should always strive for readability in your VBA code. In the small example shown in Figure 25.1, you can easily see that sFormName holds the name of a form, especially because it's used as part of the DoCmd.OpenForm statement.

## Naming variables

Every programming language has its own rules for naming variables. In VBA, a variable name must meet the following conditions:

- It must begin with an alphabetical character.
- It must have a unique name. The variable's name cannot be used elsewhere in the procedure or in modules that use the variables.
- It must not contain spaces or punctuation characters (except underscore).
- It must not be a reserved word, such as Sub, Module, or Form.
- It must be no longer than 255 characters.
