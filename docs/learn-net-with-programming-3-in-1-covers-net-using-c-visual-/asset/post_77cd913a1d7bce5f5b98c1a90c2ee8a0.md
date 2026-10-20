
The `char` data type is used to store a single character. The character must be surrounded by single quotes, like `'A'` or `'c'`:

**Example:**

```csharp
char mygrade = 'B';

Console.WriteLine(mygrade);
```

### Strings

The `string` data type is used to store a sequence of characters (text). String values must be surrounded by double quotes:

**Example:**

```csharp
string greeting = "Hello World";

Console.WriteLine(greeting);
```

## 2.10 C# Type Casting

Type casting is when you assign a value of one data type to another type.

In C#, there are two types of casting:

### Implicit Casting (automatically) - converting a smaller type to a larger type size

`char -> int -> long -> float -> double`

### Explicit Casting (manually) - converting a larger type to a smaller size type

`double -> float -> long -> int -> char`

### Implicit Casting

Implicit casting is done automatically when passing a smaller size type to a larger size type:

**Example:**

```csharp
int myint = 9;
double mydouble = myint;    // Automatic casting: int to double
Console.WriteLine(myint);    // Outputs 9
Console.WriteLine(mydouble); // Outputs 9
```

### Explicit Casting

Explicit casting must be done manually by placing the type in parentheses in front of the value:

**Example:**

```csharp
double mydouble = 9.78;
int myint = (int) mydouble;    // Manual casting: double to int
Console.WriteLine(mydouble); // Outputs 9.78
Console.WriteLine(myint); // Outputs 9
```

## 2.11 Type Conversion Methods

It is also possible to convert data types explicitly by using built-in methods, such as `Convert.ToBoolean`, `Convert.ToDouble`, `Convert.ToString`, `Convert.ToInt32` (int) and `Convert.ToInt64` (long):

**Example:**

```csharp
int myint = 10;
double mydouble = 5.25;
bool mybool = true;

Console.WriteLine(Convert.ToString(myint)); // convert int to string
Console.WriteLine(Convert.ToDouble(myint)); // convert int to double
Console.WriteLine(Convert.ToInt32(mydouble)); // convert double to int
Console.WriteLine(Convert.ToString(mybool)); // convert bool to string
```

## Get User Input

You have already learned that `Console.WriteLine()` is used to output (print) values. Now we will use `Console.ReadLine()` to get user input.

In the following example, the user can input his or hers username, which is stored in the variable `username`. Then we print the value of `username`:

**Example:**

```csharp
// Type your username and press enter
Console.WriteLine("Enter username:");

// Create a string variable and get user input from the keyboard and store it in the variable
string username = Console.ReadLine();

// Print the value of the variable (username), which will display the input value
Console.WriteLine("Username is: " + username);
```

![](img/e7ca4af023a4148a909dd82c11f81893_58_0.png)

### User Input and Numbers

The `Console.ReadLine()` method returns a string. Therefore, you cannot get information from another data type, such as `int`. The following program will cause an error:

**Example:**

```csharp
Console.WriteLine("Enter your age:");
int age = Console.ReadLine();
Console.WriteLine("Your age is: " + age);
```

The error message will be something like this:

`Cannot implicitly convert type 'string' to 'int'`

Like the error message says, you cannot implicitly convert type `'string'` to `'int'`.

Luckily, for you, you just learned from the previous chapter (Type Casting), that you can convert any type explicitly, by using one of the `Convert.To` methods:

![](img/e7ca4af023a4148a909dd82c11f81893_59_0.png)

## 2.12 C# Operators

Operators are used to perform operations on variables and values. In the example below, we use the `+` operator to add together two values:

**Example:**

```csharp
int x = 100 + 50;
```

### Arithmetic Operators

Arithmetic operators are used to perform common mathematical operations:

| Operator | Name | Description | Example | Try it |
| --- | --- | --- | --- | --- |
| `+` | Addition | Adds together two values | `x + y` | Try it * |
| `-` | Subtraction | Subtracts one value from another | `x - y` | Try it * |
| `*` | Multiplication | Multiplies two values | `x * y` | Try it * |
| `/` | Division | Divides one value by another | `x / y` | Try it * |
| `%` | Modulus | Returns the division remainder | `x % y` | Try it * |
| `++` | Increment | Increases the value of a variable by 1 | `x++` | Try it * |
| `--` | Decrement | Decreases the value of a variable by 1 | `x--` | Try it * |

### C# Assignment Operators

Assignment operators are used to assign values to variables.

In the example below, we use the assignment operator (`=`) to assign the value 10 to a variable called x:

**Example:**

```csharp
int x = 10;
```

The addition assignment operator (`+=`) adds a value to a variable:

**Example:**

```csharp
int x = 10;
x += 5;
```

| Operator | Example | Same As |
| --- | --- | --- |
| `=` | `x = 5` | `x = 5` |
| `+=` | `x += 3` | `x = x + 3` |
| `-=` | `x -= 3` | `x = x - 3` |
| `*=` | `x *= 3` | `x = x * 3` |
| `/=` | `x /= 3` | `x = x / 3` |
| `%=` | `x %= 3` | `x = x % 3` |
| `&=` | `x &= 3` | `x = x & 3` |
| `\|=` | `x \|= 3` | `x = x \| 3` |
| `^=` | `x ^= 3` | `x = x ^ 3` |
| `>>=` | `x >>= 3` | `x = x >> 3` |
| `<<=` | `x <<= 3` | `x = x << 3` |

### C# Comparison Operators

Comparison operators are used to compare two values:

| Operator | Name | Example |
| --- | --- | --- |
| `==` | Equal to | `x == y` |
| `!=` | Not equal | `x != y` |
| `>` | Greater than | `x > y` |
| `<` | Less than | `x < y` |
| `>=` | Greater than or equal to | `x >= y` |
| `<=` | Less than or equal to | `x <= y` |

### C# Logical Operators

Logical operators are used to determine the logic between variables or values:

| Operator | Name | Description | Example |
| --- | --- | --- | --- |
| `&&` | Logical and | Returns true if both statements are true | `x < 5 && x < 10` |
| `\|\|` | Logical or | Returns true if one of the statements is true | `x < 5 \|\| x < 4` |
| `!` | Logical not | Reverse the result, returns false if the result is true | `!(x < 5 && x < 10)` |

### Math.Max(x,y)

The `Math.Max(x,y)` method can be used to find the highest value of x and y:

**Example:**

```csharp
Math.Max(5, 10);
```

### Math.Min(x,y)

The `Math.Min(x,y)` method can be used to find the lowest value of x and y:

**Example:**

```csharp
Math.Min(5, 10);
```

### Math.Sqrt(x)

The `Math.Sqrt(x)` method returns the square root of x:

**Example:**

```csharp
Math.Sqrt(64);
```

### Math.Abs(x)

The `Math.Abs(x)` method returns the absolute (positive) value of x:

**Example:**

```csharp
Math.Abs(-4.7);
```

### Math.Round()

`Math.Round()` rounds a number to the nearest whole number:

**Example:**

```csharp
Math.Round(9.99);
```

## C# Strings

Strings are used for storing text.

A string variable contains a collection of characters surrounded by double quotes:

**Example:**

Create a variable of type string and assign it a value:

```csharp
string greeting = "Hello";
```

### String Length

A string in C# is actually an object, which contain properties and methods that can perform certain operations on strings. For example, the length of a string can be found with the `Length` property:

**Example:**

```csharp
string txt = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
Console.WriteLine("The length of the txt string is: " + txt.Length);
```

### Other Methods

There are many string methods available, for example `ToUpper()` and `ToLower()`, which returns a copy of the string converted to uppercase or lowercase:

**Example:**

```csharp
string txt = "Hello World";
Console.WriteLine(txt.ToUpper());    // Outputs "HELLO WORLD"
Console.WriteLine(txt.ToLower());    // Outputs "hello world"
```

### String Concatenation

The `+` operator can be used between strings to combine them. This is called concatenation:

**Example:**

```csharp
string firstname = "John ";
string lastname = "Doe";
string name = firstname + lastname;
Console.WriteLine(name);
```

### String Interpolation

Another option of string concatenation, is string interpolation, which substitutes values of variables into placeholders in a string. Note that you do not have to worry about spaces, like with concatenation:

**Example:**

```csharp
string firstname = "John";
```
