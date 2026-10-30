
## Project Files

VB project files, which have the extension .vproj and .vproj.user, are text files that store configuration settings, the names of the files needed for the project, and references to library routines needed by the project. You can examine and modify the project file with a text editor (very carefully).

## VB Files

All VB code, including general classes, Windows Form classes, and code files, are stored in files with a .vb extension. A .vb file is sometimes referred to as a module, although, technically speaking, a module in VB is defined by Module / End Module statements.

A single .vb file can hold one or more classes. Or a file can consist only of sub procedures and functions to be called by classes defined in other files.

A .vb file that is used to define a Windows Form has a companion resource file with an extension of .resx and a .Designer.vb file that contains the Windows designer-generated code. The resource file holds strings of text and any graphics or other resources needed to render the form on the screen.

For a Web application, the form files have the extension .aspx. The .aspx file is used to create the form and controls, which will be rendered with HTML. The companion file, the .aspx.vb file, holds the VB code for the form. This code file is called the code-behind file.

By default, some of the files in a solution are not shown in the Solution Explorer. You can display all files by clicking on the Show All Files button at the top of the Solution Explorer window.

## Data Types, Variables, and Constants

The data values that you use in a VB project may be variables or constants. They may be stored and manipulated as one of the intrinsic data types, a structure, or an object based on one of the built-in classes or classes that you write. The intrinsic data types in VB are based on classes and have properties and methods. You can see these by typing a variable name and a period—IntelliSense will pop up with the list of properties and methods.

## Data Types

| Data type | Use for | Storage size in bytes |
|---|---|---|
| Boolean | True or False values. | 2 |
| Byte | 0 to 255, binary data | 1 |
| Char | Single Unicode character | 2 |
| Date | 1/1/0001 through 12/31/9999 | 8 |
| Decimal | Decimal fractions, such as dollars and cents. | 16 |
| Single | Single-precision floating-point numbers with six digits of accuracy. | 4 |
| Double | Double-precision floating-point numbers with 14 digits of accuracy. | 8 |
| Short | Small integer in the range -32,768 to 32,767 | 2 |
| Integer | Whole numbers in the range -2,147,483,648 to +2,147,483,647 | 4 |
| Long | Larger whole numbers. | 8 |
| String | Alphanumeric data: letters, digits, and other characters. | varies |
| Object | Any type of data | 4 |

## Selecting the Data Type

Use String data type for text characters; also for numbers that are used for identification, such as part numbers, social security numbers, and ID numbers. As a general rule, do not use numeric data types for numbers unless you plan to calculate with the numbers. In VB, strings are immutable, which means that once created, they cannot be changed. Each time that your code makes changes to a string, behind the scenes a new string is created for the new value. You also can use Char for single-character text fields.

When dealing with whole numbers, use Integer for any values that you don't expect to surpass the range limit (see table above). For example, make counters and ages Integer. Use Long for whole numbers that may be larger than the limit. Use Byte only for compatibility with routines that require it, such as reading byte data from a file.

For fractional values, you can choose Single, Double, or Decimal. Single and Double are stored as floating-point numbers, which can have some rounding errors when working with decimal fractions, such as dollars and cents. Use Decimal for dollar amounts as well as other values stored in tenths and hundredths, such as interest rates or temperatures.

## Variables

You declare variables using the Dim statement (for dimension), or one of the other declaration statements that define the accessibility of the variable, such as Public, Private, Friend, or Static. A variable name (identifier) can be as long as you like (up to 16,383 characters); may consist of letters, digits, and underscores; cannot contain any spaces or periods; cannot be a VB keyword, and must begin with a letter.

```
Dim[Public|Private|Static] VariableName As DataType
```

You can assign an initial value to a variable as you declare it, and you can declare multiple variables on one statement and all will have the assigned data type.

## Examples

```
Dim NameString As String
Public TotalDecimal As Decimal
Private CountInteger As Integer = 1
Dim MyForm As Form
Static EventCounter As Integer
Dim CountInteger, IndexInteger As Integer    ' Two Integer variables.
Dim CompanyNameString As String = "Amalgamated Programming, Inc."
```

## Naming Conventions

Good programming practice dictates that variable names should always be meaningful. Include the data type or class in the name. Use Pascal casing, starting the name with an uppercase letter and each word with a capital letter.

## Examples

- AllDoneBoolean
- SalesAmountDecimal
- FirstNameString
- NameTextBox
- VideosComboBox

## Constants

Declare a constant for a value that will not change during program execution. The naming rules for constants are the same as for variables. However, this text uses the widely used naming convention of all uppercase names with underscores to separate words.

```
Const COMPANY_NAME_String As String = "R n R - For Reading and Refreshment"
Const TYPE_ONE_Integer As Integer = 1
```

## Declaring Numeric Constants

VB is a strongly typed programming language. Although you can choose to ignore the typing (see “Option Explicit and Option Strict” later in this appendix), you should always be aware of the data type. When you declare a numeric constant, such as 100 or 125.59, VB assigns a data type. By default, any whole number is created as Integer and any fractional value is created as Double. If you want the constant to be another data type, add a type-definition character to the right end of the number. For example: 125.55D for Decimal data type or

125.5F for Single (the F stands for floating point). The type-declaration characters are

Decimal    D
Double     R
Integer    I
Long       L
Short      S
Single     F

## Intrinsic Constants

Intrinsic constants are system-defined constants that reside in the .NET class library. You must specify the class or group name to use the constants. Some examples of helpful constants are Color.Red, Color.Blue, Color.Orange (and dozens more); ControlChars.NewLine; ControlChars.LineFeed; MessageBox-Buttons.YesNoCancel; and MessageBoxIcons.Question. IntelliSense is a great help; just type the group name and a period, and all of the available choices pop up for your selection.

## Scope and Lifetime

See Chapter 2 for a review of scope and lifetime. The scope of variables and constants has changed from VB 6.

VB scope may be block-level, local (procedure-level), module-level, or namespace-level.

## Public, Private, and Static Variables

The form for a Dim statement is

```
{Dim|Public|Private|Friend|Protected|Protected Friend|Static} VariableName As DataType
```

The default is Private, so if you use either the Dim or Private keyword, the variable is Private. Public variables are available to any other object and can violate encapsulation rules. Private variables are available only to the class in which they are declared; Protected variables are available to the current class and any classes that inherit from the current class. Friend variables are available to any classes in the current application. Protected Friend variables are a combination of Protected and Friend—they are available to any classes that inherit from the current class in the current application.

Static variables are local variables with a lifetime that matches the module rather than the procedure. If you declare a variable as Static, it is not destroyed each time the procedure exits. Instead, the variable is created once the first time the procedure executes and retains its value for the life of the module. You can use a static variable to maintain a running count or total, as well as keep track of whether a procedure has executed previously.
