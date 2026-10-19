
Step 1-14: Double click btnExit to create the Click event handler. Then delete the event handler by first deleting it from the Properties window, and then deleting the code for the event handler, including the header, the braces (and code, if any, within the braces) from the Code window.

Now you are ready to move to phase 5: Write and test the code.

## Review Questions

+   1.16 What is a namespace?
+   1.17 What does the using directive specify?
+   1.18 What is a method?
+   1.19 What is an event handler?

## 1.6 Introductory Programming Concepts

To help you understand some basic programming concepts, let’s first look at the completed code, shown in Figure 1-18, to compute the cost for an order of ice cream.

Figure 1-18: Code to compute cost

```
private void btnComputeCost_Click(object sender, EventArgs e)
{
    // Compute the total cost for an order of icecream:
    
    // Declare variables to hold input data and computed results
    int scoops;
    double unitPrice, cost;
    
    //Get input data from Text Boxes:
    scoops = int.Parse(txtScoops.Text);
    unitPrice = double.Parse(txtUnitPrice.Text);
    
    // Compute result
    cost = unitPrice * scoops;
    
    // Display Result
    lblCost.Text = cost.ToString("C");
}
```

As you can see from the code, the method includes three segments corresponding to the three subtasks that were identified earlier:

+   Get number of scoops and unit price (lines 29 & 30)
+   Compute cost (line 33)
+   Display cost (line 36)

Note that the line numbers are not part of the code. They are inserted using a setting in Visual Studio for ease in reference to a statement (select Tools, Options, Text Editor: C# and check Line Numbers).

Let’s look closely at the statements in this program.

### Comments

Line 22: //Compute the total cost for an order of ice cream:

Lines starting with // are comments for the programmers and are ignored by the compiler.

You may comment multiple lines by placing the lines between /* and */, as in Figure 1-19.

### Figure 1-19: Commenting multiple lines

```
22    /*Compute the total cost for an order of icecream
23      using the formula: cost = unitPrice * NumberOfScoops:
24      Declare variables to hold input data and computed results*/
```

You may comment out a set of lines by highlighting the lines (drag the mouse pointer over them) and then clicking the Toolbar button Comment out the selected lines, shown in the following image:

![](img/143bad48262566137acc9c41f668a88f_41_0.png)

The button to the right would uncomment the selected lines.

## 1.7 Data Types

Lines 25 and 26 declare variables and specify what types they are:

+   Line 25: int scoops;
+   Line 26: double unitPrice, cost;

In order to understand the above statements and the rest of the program, we will take a closer look at data types and variables.

Data used in a program can be grouped broadly into the following types:

+   **Integer:** An integer is a whole number (e.g., 255677, -54).
+   **Nonintegers or reals:** A real number has one or more decimal places (e.g., 255677.75; -0.255).
+   **Text:** Text data include **character** type that consists of an individual character (e.g., 'A'; 'B') and **string** type that consists of a group of characters, including alphabetical characters, numeric digits and special characters (e.g., "John Smith"; "P410-2023-3180-05").
+   Notice that a character is enclosed in single quotes, and a string is enclosed in double quotes.
+   **Boolean:** A Boolean has the value true or false.
+   **Date/Time:** Date and time are enclosed in a pair of pound signs, as in #05/25/2016 02:30:00 PM#.

Let’s look at the different C# types for integers and reals.

### Integer types

Table 1-3 shows the different integer types in C#. Note that C# is case sensitive. That means the key words for data types, like short and int, are case sensitive. So, “Short” and “Int” are invalid key words.

Table 1-3: Built-in C# data types for Integers

| C# key word | Size (memory used) | Range of values |
| sbyte | 8 bits | -128 to 127 |
| short | 16 bits | -32,768 to 32,767 |
| int | 32 bits | -2,147,483,648 to 2,147,483,647 |
| long | 64 bits | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| char | 16 bits | 0 to 65535 |

There are additional “unsigned” data types, byte, ushort, uint and ulong, which can store only positive, but larger, integers with maximum size close to double that of signed integers. For example, uint type variables can hold values up to 4,294,967,295, whereas the maximum for int type is only 2,147,483,647.

The size shows the memory needed to store the data, and the range shows the range of values that can be stored in the variable. Larger data types take more memory, as reflected in the size.

Note that character data (denoted by the C# key word char) is represented by integers using one of the popular standards called Unicode that allows representation of 65,535 different characters from different languages.

### C# versus .Net Types

The names of basic data types in C# are different from those in .Net Framework. However, there is direct correspondence between them. For example, int type in C# is the same as System.Int32 in .Net, and long in C# is the same as System.Int64.

### Noninteger (real) types

Table 1-4 shows the data types for non-integers.

### Table 1-4: C# noninteger types

| C# keyword | Size | Range of values | Precision | How the number 123456789012.345678901234567890 may be represented |
|---|---|---|---|---|
| float | 32 bits | ±1.5 × 10⁻⁴⁵ to ±3.4 × 10³⁸ | 7 digits | 0.1234568 x 10¹² |
| double | 64 bits | ±5.0 × 10⁻³²⁴ to ±1.7 × 10³⁰⁸ | 15 digits | 0.123456789012346 x 10¹² |
| decimal | 128 bits | ±1.0 × 10⁻²⁸ to ±7.9 × 10²⁸ | 28-29 digits | 123456789012.345678901234567800 |

As indicated by the ranges, float and double can store larger numbers than decimal type. They also take less memory. But float and double cannot represent all noninteger numbers exactly (due to the method used by them to represent numbers), making them less suitable than decimals for financial calculations.

Decimal type, in general, can represent real numbers exactly, and it has better precision than float and double. Hence, as stated earlier, decimal is better suited for financial calculations where exact representation is important. However, decimal type takes more memory and is slower to work with than float and doubles. Because decimal has a lower range, it may not be appropriate for some scientific calculations.

The C# types, float and double, use a method of representation called floating point method to approximate a wide range of values to a fixed number of significant digits. Therefore, float and double also are referred to as floating point types.

### string type

The C# type string represents a combination of zero or more characters. “John Smith” and “P410-2023-3180-05” are examples of string type data. Note that string type data is enclosed in quotes.

### bool type

The C# type bool represents Boolean data that include the values true and false.

### DateTime type

C# doesn’t have a data type for dates and times. The .Net base type DateTime is used to represent dates and/or times.

## Review Questions

1.20 What is the appropriate data type to represent student GPA?

1.21 Which real data type is best suited for financial calculations where exact representation of numbers is important?

1.22 What are the advantages of float and double types compared to decimal?

## 1.8 Working with Variables

Programs typically use variables to hold data. A simple variable holds one piece of data, and more complex types like an array can hold a set of data. In general, we will use the term “variable” to denote a simple variable.

A variable is a location in computer memory where it holds data while the program is running. The program accesses the location using the name given to the variable.

For variables, C# requires that you specify what type of data will be stored in each variable.

### Creating (Declaring) Variables

Variables are created by specifying the type and a name of the variable. The statement shown below from Line 25 in Figure 1-18 creates a variable named scoops that is of int type:

```
int scoops;
```

When the program is run, the above statement creates a variable named scoops in computer memory to hold an int type integer data. Because we haven’t assigned any value to scoops, by default, the value zero is stored in the variable, as represented below:

![](img/143bad48262566137acc9c41f668a88f_44_0.png)

You may declare two or more variables of the same type in a statement, as in line 26 in Figure 1-18:

```
double unitPrice, cost;
```

This statement creates two variables, unitPrice and cost, to hold double type floating point data.

Note that a semicolon is required to denote the end of each C# statement.

### Guidelines for naming variables

Variable names must start with a letter, and can contain only letters, numbers or the underscore “_” character.

The convention in C# is to use the Camel Case: The first letter of a variable is lowercase, and the first letter of subsequent words, if any, are capitalized, as in totalCost and averageRetailPrice.
