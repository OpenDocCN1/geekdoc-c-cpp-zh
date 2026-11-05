
> Do not place a comment on every line or with every variable declaration because it creates unreadable code. It is best to include comments when a segment of code needs further explanation.

Each identifier in Example 2-3 consists of two or more words. The second and subsequent words begin with an uppercase character. This naming convention is used throughout the textbook for variable and object names. The first character of the identifier begins with a lowercase character.

Class and method names, both user-defined and Framework class library (FCL) class identifiers, begin with an uppercase character. Constants, which are covered later in this chapter, are named with all uppercase characters, using the underline character to separate words. This is the standard style used by C# programmers.

> Style is composed of a set of personal choices adopted by programmers. If you are new to programming, you might want to follow the textbook's style for selecting identifiers; however, your instructors might have different styles that they recommend. Another common naming convention is to separate words with an underscore. The most important thing to remember is that after selecting a style, you should use it consistently.

## FLOATING-POINT TYPES

If you need to keep the decimal portion, the value cannot be stored in an integral data type, such as an int. Floating-point values can be specified in scientific notation with an exponent or in standard decimal notation. Very large or small numbers can be specified. The general form of exponential syntax is:

```
n.n e±P
```

With the scientific notation syntax in the preceding example, n is the decimal number; P is the number of decimal positions to move left or right; and the + or – indicate the direction the decimal should be moved. A plus sign indicates that the decimal is moved P positions to the right to form the standard decimal equivalent value. The syntax rules in C# allow the e to be uppercase or lowercase. The ± in the notation indicates that a +, –, or neither can be added. If there is no + or –, + is assumed. Example 2-4 shows examples of converting from scientific to standard decimal notation.

### Example 2-4

- 3.2e+5 is equivalent to 320000
- 1.76e-3 is equivalent to .00176
- 6.892e8 is equivalent to 689200000

Because the first value includes an "e+5", the decimal is moved to the right five positions. The second statement in the preceding examples moves the decimal position three positions to the left. The last statement moves the decimal to the right eight positions, which places five significant zeros onto the end of the value.

As Table 2-10 indicates, a value with up to 15 to 16 decimal places can be placed in a double. The floating-point types conform to IEEE 754 specifications. For more information, you can read about the IEEE standard at the Web site http://standards.ieee.org/. The following are examples of floating-point variable declarations.

### Table 2-10 Values and sizes for floating-point types

| Type | Numeric range | Precision | Size |
|---|---|---|---|
| float | ±1.5 × 10⁻⁴⁵ to ±3.4 × 10³⁸ | 7 digits | 32-bit |
| double | ±5.0 × 10⁻³²⁴ to ±1.7 × 10³⁰⁸ | 15–16 digits | 64-bit |

### Example 2-5

```
double extraPerson = 3.50;    // extraPerson originally set
                             // to 3.50
double averageScore = 70.0;   // averageScore originally set
                             // to 70.0
double priceOfTicket;         // cost of a movie ticket
double gradePointAverage;     // grade point average
float totalAmount = 23.57f;   // note that the f must be placed after
                             // the value for float types
```

Notice that all but one of the declarations in Example 2-5 uses double. In C#, double is the default type for floating-point numbers. When a compile-time initialization is included, no suffix is required if you initialize a double variable. In the case of the float, it is necessary to suffix the number with an f or F; otherwise, the number is assumed to be a double. If you fail to suffix the number with an f or F and assign it to a float variable, you get a syntax error similar to that shown in Figure 2-6.

![](img/e33ae760e23d89eac66541252ad65de8_118_0.png)

Figure 2-6  Syntax error for failing to use F suffix

The **double** type is used throughout the textbook for all numbers that require a fractional value.

## DECIMAL TYPES

The **decimal** value type is new to modern programming languages. It is appropriate for storing monetary data items because it allows both integral (whole) numbers and a fractional portion. It provides for greater precision than what is found with floating-point types because 128 bits are used to represent the value.

Numbers ranging from negative −79,228,162,514,264,337,593,543,950,335 to positive 79,228,162,514,264,337,593,543,950,335 can be stored in a **decimal** value type. As you can see in Table 2–11, 28 to 29 digits are possible with the **decimal**.

### Table 2-11 Value and size for decimal data type

| Type | Numeric range | Precision | Size |
|---|---|---|---|
| `decimal` | 1.0 × 10^-28 to 7.9 × 10^28 | 28–29 significant digits | 128 bits |

As is the case with the **float** type, it is necessary to attach the suffix m or M onto the end of a number to indicate **decimal**, as shown in Example 2–6. Without the suffix, the number is treated as a **double**. Again, a syntax error message is issued if you try to do compile-time initialization or assign a number to a **decimal** variable without the suffix. No automatic conversion occurs.

### Example 2-6

```
decimal endowmentAmount = 33897698.26M;
decimal deficit;
```

![](img/e33ae760e23d89eac66541252ad65de8_119_0.png)

Never place commas, dollar signs, or any other special formatting symbols with numbers when they are assigned to value types.

## BOOLEAN VARIABLES

Boolean is based on true/false, on/off logic. If you look back at the value type hierarchy in Figure 2–5, you see that Boolean inherits from the Value and Struct classes, but not from the Numeric type. The only Boolean type in C# is `bool`. A `bool` variable can have a value of either `true` or `false`. One example of the `bool` type being very useful is in determining when all data has been processed. The variable can be declared as shown in Example 2–7.

### Example 2-7

```
bool undergraduateStudent;
bool moreData = true;        // used to indicate when all data is
                            // processed. Originally set to true
```

The `bool` type will not accept integer values such as 0, 1, or −1. The keywords `true` and `false` are built in to the C# language and are the only allowable values.

![](img/e33ae760e23d89eac66541252ad65de8_119_1.png)

Some languages such as C++ allow Boolean types to hold integers. C# does not.

In addition to numeric and Boolean, there are two other value types: enumeration and structures. These allow you to define your own custom classes. They will be used as you advance in your software development.

## DECLARING STRINGS

All the types previously discussed were value types. As shown in Figure 2–3, the .NET common type system also includes reference types. The memory location of value types actually contains the data. With reference types, data is not stored directly in the memory location; instead, the memory location contains a reference to the location in which the data is stored.

C# has two built-in reference types: `string` and `object`. The `string` type represents a string of Unicode characters. Example 2–8 shows how `string` variables are declared. The second and third declarations also include compile-time initializations.

### Example 2-8

```
string studentName;
string courseName = "Programming I";
string twoLines = "Line1\nLine2";    // newline escape sequence
    // character included
```

The other built-in reference type is object. This is probably the most important type of all because every type inherits characteristics from it. In Chapter 3, you will investigate the object class when you begin writing your own methods.

![](img/e33ae760e23d89eac66541252ad65de8_120_0.png)

All types inherit the methods ToString( ), Equals( ), Finalize( ), and GetHashCode( ) from the object class.

## MAKING DATA CONSTANT

When you add the keyword const to a declaration, it becomes a constant. Constants are convenient for assigning a value to an identifier; const forces the functionality of not allowing the value to be changed. Similar to a variable, the value stored in the memory location can be used throughout the program. However, the value cannot be altered. The general form of constant syntax is:

```
const type identifier = expression;
```

Some examples of constant declarations are shown in Example 2-9.

### Example 2-9

```
const double TAX_RATE = 0.0675;
const int SPEED = 70;
const char HIGHEST_GRADE = 'A';
```

![](img/e33ae760e23d89eac66541252ad65de8_120_1.png)

An advantage of defining a constant is that the value need only be assigned once, during declaration. A constant can be used in many statements. If the value must be changed, only one change is required in the program and that is at the constant declaration location. After that change is made, the program must be recompiled.

To call attention to the fact that the identifier TAX_RATE is a constant instead of a variable, all capital letters are used. To provide a separator between words, the underscore character is used. This is the standard convention used by programmers for naming constants.
