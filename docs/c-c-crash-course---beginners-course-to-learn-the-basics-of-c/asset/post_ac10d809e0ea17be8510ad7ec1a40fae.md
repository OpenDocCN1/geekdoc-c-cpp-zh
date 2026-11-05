
## The Variables

You can use a variable to store, retrieve, and modify changeable data. As a programmer, you need to use variables in storing and processing information.

### The Characteristics of a Variable

A variable has the following characteristics:

- Name (also known as "Identifier")
- Data Type
- Value (i.e. the information you want to store).

Variables are sections of computer memory that have a name. They store values and allow a computer program to access their contents. You may place a variable inside the stack (i.e. the working memory of your computer program) or within the program’s dynamic memory.

Characters, Booleans, and Integers are known as value types since they keep their data within the program’s stack. On the other hand, strings, arrays, and objects are known as "reference types" because they don’t hold the values inside them. Instead, they serve as markers that point to the part of computer memory where the data is stored.

### How to Name a Variable

You need to name your variables before using them. The variable’s name serves as an identifier: it helps the program in locating and specifying the variable. C# allows you to choose variable names freely. However, just like any other language, C# has some rules regarding variable names. These rules are as follows:

- You may use an underscore (i.e. "_"), letters, and numbers to create a variable name.
- You can’t use a number to start the name. Thus, FirstSample is valid while 1stSample is not.
- You can’t use C# keywords in naming your variables. This simple rule prevents compilation and runtime errors in your programs. If you really want to use keywords for your variables, you may begin the name using the "@" symbol (e.g. @bool, @int, @char, etc.).

### How to Declare a Variable

You should declare a variable before using it. Here are the things you need to do when declaring a variable:

- 1. Specify the variable’s data type (e.g. char)
- 2. Specify the variable’s name (e.g. sample)
- 3. Set the variable’s initial value. This step is completely optional.

The format for variable declarations is:

```csharp
data_type name = initial_value;
```

Here are some samples of valid variable declarations:

```csharp
int year = 2000;
```

```csharp
string yourname = "John Doe";
```

```csharp
char test = 'x';
```

Important Note: You need to end each of your C# statements using a semicolon. If you’ll forget to add even a single semicolon character, your programs will generate undesirable and/or unexpected results.

### How to Assign a Value

Just like any other computer language, C# allows you to assign a value to a variable. This process, known as “value assignment”, requires you to use the equals sign. Programmers refer to this symbol as the “assignment operator”. Write the variable’s name on the left side of the operator. Then, specify the value you want to assign on the other side. Check the following examples:

```csharp
test = 'x';
```

```csharp
yourname = "John Doe";
```

### How to Initialize a Variable

In programming, “initialization” is the process of assigning a value to a new variable. Thus, you’ll set this “initial value” while declaring a variable.

### The Default Value of a Variable

If you won’t assign any value for your variable, C# will perform an automated initialization (i.e. it will assign a default value to the empty variable). The following tables will show you the default value of each data type:

| Data Type | Default Value |
|---|---|
| sbyte | 0 |
| byte | 0 |
| short | 0 |
| ushort | 0 |
| int | 0 |
| uint | 0u |
| long | 0L |
| ulong | 0u |
| float | 0.0f |
| double | 0.0d |
| decimal | 0.0m |
| bool | false |
| char | '\u0000' |
| string | null |
| object | null |

The code given below will show you how to declare variables and assign values.

```csharp
// This is an example
byte years = 10;
short days = 31;
decimal pi = 3.14;
bool isitasty = true;
char sample = 'x';
string animal = "dog";
```

Important Note: Lines that begin with two forward slashes (i.e. //) are “comments”. In programming, comments are descriptive text added to the code to improve its readability. Language compilers ignore these lines. Thus, comments won’t affect the functionality of your computer programs.

### Values and References

C# programmers divide data types into two categories: value types and reference types.

A value type exists inside the execution stack of a program. Additionally, it holds the value stored by the programmer. The Value Type category consists of the Booleans, Characters, and Integers. The memory assigned to these data types becomes available once the program finishes its code execution. For instance, the variables within the Main() method of your program will be emptied once the program is closed.

A reference type, on the other hand, stores an address (i.e. a reference) in the program’s stack. This address points to the location of the needed value. Basically, a reference type assigns dynamic memory during its declaration. It also frees up some memory once the program no longer needs it.

### The Literals

Literals are the values specified in a program’s source code. The example given below will illustrate this idea:

```csharp
bool isitdelicious = false;
short income = 22000;
char firstletter = 'c';
byte ten = 10;
int prize = 250000;
```

In this example, the literals are false, 22000, 'c', 10 and 250000. These are values that you’ll add directly to the program’s code.

### The Different Kinds of Literals

C# supports the following kinds of literals:

- Real
- Integer
- String
- Character
- Boolean

Let’s discuss each of these literals in detail:

### Real

A real literal has a sign (i.e. + or -), a suffix, a prefix, and a decimal point. You should use this kind of literal for double, float, and decimal values. C# allows you to write real literals in their exponent form. Here are the suffixes that you can apply on real literals:

- F – This suffix represents float values.
- D – Use this suffix to indicate double values.
- M – This letter indicates decimal values.
- E – Use this letter for exponential values. For instance, “e4” means you need to multiply the integer by 10⁴.

### Integer

An integer literal consists of a prefix, a suffix, a sign (i.e. + or -), and a set of digits. You can use prefixes to add numbers in your code as decimals or hexadecimals. Here are the prefixes and suffixes that you can use in C#:

- 0X (e.g. 0XA6F2) – Use this prefix to indicate a hexadecimal value.
- U (e.g. 119U) – This suffix represents unsigned int (uint) or unsigned long (ulong) values.
- L (e.g. 360L) – Use this suffix for “long” values.

Important Note: C# will tag integer literals as “int” if you won’t use any suffix. Also, the letters (i.e. L, U and X) are not case-sensitive.

### String

Use this literal for string values. Basically, a string literal is a set of characters placed within a pair of double quotes (e.g. “sample”).

Important Note: In the C# language, you may use the “@” symbol to create quoted (or verbatim) strings. Programmers use these strings for naming file paths.

### Character

A character literal is a single character enclosed by a pair of single quotes (e.g. 'z'). Use character literals to set values that belong to the “char” type. Additionally, you may write a character literal as:

- a single character (e.g. 'X')
- a code for a special character (e.g. '\u0067')
- an escape code (see below)

Escape Codes – These are special character sequences that add characters to your source code. In general, the characters involved here cannot be added straight to the program’s codes.

C# prevents you from adding some characters straight to your programs. Some of these characters are: tabs, newlines, backslashes, quotation marks, etc. The following list will show you the most popular escape codes in C#:

- \n – Newline Character
- \t – Tab Character
- \' – Single Quotation Mark
- \" – Double Quotation Mark

### Boolean

There are only two types of Boolean literals: true and false. You can only assign one of these values when working with a “bool” (i.e. Boolean) variable. The code snippet given below will show you how to declare a Boolean literal:

```csharp
bool answer = false;
```
