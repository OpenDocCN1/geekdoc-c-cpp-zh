
While developing programs in C#, several times you need to perform conversions between int and string data types. The **ToString()** and **Parse()** methods are two predefined methods that allow you to convert an int type into string type and vice-versa.

In C#, the **ToString()** method allows you to convert int data type (and other data types) to its string equivalent. The following code snippet shows how to use the ToString() method to assign the value stored in the int variable, Age, to a variable, strAge, of the string type:

```
int Age = 27;
string strAge = Age.ToString();  //strAge is equal to "27"
```

To convert the string type to the int type, you can use the Parse() method. In the following code snippet, the value of the string type variable, Phone, is converted to int type by using the Parse() method:

```
string Phone = "9898981111";
int PhoneNumber = int.Parse(Phone);  //PhoneNumber is equal to 9898981111
```

![](img/9862a98a1a2d3bb14334137965a1ec60_294_0.png)

> The System namespace contains a class, called Convert, which provides several methods to convert the values of predefined data type to another. The methods provided by the Convert class include ToString(), ToChar(), ToBoolean(), and ToInt32().

You have learned about data types and data type conversions. Data types are generally specified for variables and constants; therefore, let’s now learn about variables and constants.

## Describing Variables and Constants

A variable is a block of memory where data or value of a particular data type is stored. Every variable has a name, data type, and an initial value. The name or identifier of the variable allows you to access the memory location where its value is stored. The data type of the variable informs the compiler about the size of memory that the variable occupies. In addition, the data type indicates the type of values the variable can store. The value that you store in a variable can be changed or modified any number of times in the program.

Note that the name of a variable has to be unique in a given scope. When you give a name to a variable, you need to remember the following points:

- The variable name can contain only letters, digits, and the underscore character (_).
- The variable name cannot start with a digit.
- The variable name in uppercase and lowercase is distinct; for example, salary and SALARY are two different variables. This is because C# is a case-sensitive language.
- The variable name cannot be a keyword.
- The variable name cannot contain whitespaces.

The following is a list of some valid variable names in C#:

- salary
- total_amount
- yearly_cost

The following is a list of some invalid variable names in C#:

- total#amount
- double
- 9number

In the preceding list, total#amount is not a valid variable name because it contains the hash character (#), which cannot be used in a variable name. double is also an invalid variable name as it is a reserved keyword that cannot be used as a variable name. Similarly, 9number cannot be used as a variable name as it starts with a digit.

Besides variables, C# also allows you to create constants, which are placeholders for values that do not change during the execution of the program. Once you have assigned a value to a constant, you cannot modify the value of the constant later in the program. Therefore, you can use constants to store static values, for instance, value of Pi.

In this section, you now learn to perform the following tasks:

- [ ] Declare variables
- [ ] Initialize variables
- [ ] Declare variables of the nullable type (that can contain null values)
- [ ] Declare constants

Let’s learn to perform each of these tasks, one by one.

### Declaring Variables

In C#, you need to declare a variable before using it in a program. Declaring a variable is necessary because by declaring the variable in a program, you create the variable. As a result, the compiler is aware of the variable and identifies it wherever it is used in the program. While declaring a variable, you need to specify the name and data type of the variable.

The syntax to declare a variable is given as follows:

```
Data_Type Variable_Name;
```

In the preceding syntax,

- [ ] **Data_Type:** Refers to the data type of the variable to be created
- [ ] **Variable_Name:** Refers to the name of the variable to be created

The following code snippet shows examples of variable declaration in C#:

```
string FirstName;
int Age;
int Weight;
```

In the preceding code snippet, three different variables are declared by using three different statements. The first statement declares a variable, named **FirstName**, of the string data type. The second statement declares another variable, named **Age**, of the int data type. Similarly, the third statement declares a variable, named **Weight**, of the int data type.

You can declare multiple variables in the same statement. In addition, if you have multiple variables of the same data type, then you can declare them in the same statement as a comma-separated list by specifying the name of the data type only once.

The syntax to declare multiple variables of the same data type is given as follows:

```
Data_Type Variable_Name1, Variable_Name2, . . ., Variable_NameN;
```

In the preceding syntax,

- [ ] **Data_Type:** Refers to the data type of the variables
- [ ] **Variable_Name1, Variable_Name2, . . ., Variable_NameN:** Refers to the names of the individual variables

The following code snippet shows how to declare multiple variables of the same data type in a single statement:

```
string FirstName;
int Age, Weight;
```

In the preceding code snippet, the **FirstName** variable is declared separately in the first statement. However, in the second statement, the **Age** and **Weight** variables are declared together in one statement.

After declaring a variable, you need to initialize the variable with a value, it means, you need to assign a value to the variable. Let’s now learn how to initialize variables in C#.

### Initializing Variables

In C#, you cannot use a variable unless you assign a value to it. Variable assignment refers to the process of providing values to a variable. When you assign the first or initial value to a variable, it is referred to as initializing the variable. After initializing a variable, you can use the variable in the program as many times as you want. You can also change or replace the initial value and assign a new value to the variable.

The syntax to assign values to a variable is as follows:

```
VariableName = Value;
```

In the preceding syntax,

- **Variable_Name:** Refers to the name of the variable
- **=:** Refers to the assignment operator
- **Value:** Refers to the value that is to be stored in the variable

The following code snippet shows how to assign values to variables:

```
FirstName = "John";
Age = 27;
Weight = 68;
```

In the preceding code snippet, the **FirstName** variable is assigned the value, **John**. Similarly, the **Age** and **Weight** variables are assigned the values, 27 and 68, respectively.

If you need to assign a value to multiple variables, then you can combine their assignments, as shown in the following code snippet:

```
Age = Weight = 55;
```

In the preceding code snippet, the **Age** and **Weight** variables are assigned the same value, 55.

You can also assign values to variables at the time of their declaration. To do so, you just need to append the assignment operator and the value to the declaration. For example, you can assign values to the **FirstName**, **Age**, and **Weight** variables while declaring these variables, as shown in the following code snippet:

```
string FirstName = "John";
int Age = 27;
int Weight = 68;
```

Or,

```
string FirstName = "John";
int Age = 27, Weight = 68;
```

Table 1.5 lists some examples of variable initialization at the time of declaration:

| Variable Declaration | Variable Name | Data Type | Initial Value |
|---|---|---|---|
| `int Marks = 85;` | Marks | int | 85 |
| `bool Status = false;` | Status | bool | false |
| `float Height = 164.5F;` | Height | float | 164.5F |
| `char Gender = 'F';` | Gender | char | F |
| `decimal CostPrice = 2.34M;` | CostPrice | decimal | 2.34M |

Let’s now discuss how to declare variables of the nullable type.

### Declaring Variables of Nullable Type

In C#, variables of value types cannot contain the null value, which is a keyword that indicates nothing or undefined value. However, when you work with databases, you may require using the null value with variables. For such a situation, C# provides the nullable type, which is represented by the predefined `System.Nullable<T>` struct.

It is important to note that the nullable type can only be applied to variables declared as value type. This implies that variables of the nullable type can contain the range of values predefined for the underlying value type along with the null value. For example, if you declare a variable as nullable of Int32 (`Nullable<Int32>`), then you can assign a value ranging from
