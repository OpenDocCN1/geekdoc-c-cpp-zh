
## SR 2.5 What output is produced by the following code fragment?

```
System.out.print ("Ready ");
System.out.println ();
System.out.println ("Set ");
System.out.println ();
System.out.println ("Go ");
```

## SR 2.6 What output is produced by the following statement? What is produced if the inner parentheses are removed?

```
System.out.println ("It is good to be " + (5 + 5));
```

## SR 2.7 What is an escape sequence? Give some examples.

## SR 2.8 Write a single println statement that will output the following exactly as shown (including line breaks and quotation marks).

> "I made this letter longer than usual because I lack the time to make it short."  
> Blaise Pascal

## 2.2 Variables and Assignment

Most of the information we manage in a program is represented by variables. Let’s examine how we declare and use them in a program.

### Variables

A variable is a name for a location in memory used to hold a data value. A variable declaration instructs the compiler to reserve a portion of main memory space large enough to hold a particular type of value and indicates the name by which we refer to that location.

Consider the program PianoKeys, shown in Listing 2.5. The first line of the main method is the declaration of a variable named keys that holds an integer (int) value. The declaration also gives keys an initial value of 88. If an initial value is not specified for a variable, the value is undefined. Most Java compilers give errors or warnings if you attempt to use a variable before you’ve explicitly given it a value.

The keys variable, with its value, could be pictured as follows:

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_92_0.png)

> **KEY CONCEPT**  
> A variable is a name for a memory location used to hold a value of a particular data type.

### Local Variable Declaration

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_93_0.png)

### Variable Declarator

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_93_1.png)

A variable declaration consists of a Type followed by a list of variables. Each variable can be initialized in the declaration to the value of the specified Expression. If the final modifier precedes the declaration, the identifiers are declared as named constants whose values cannot be changed once set.

Examples:

```
int total;
double num1, num2 = 4.356, num3;
char letter = 'A', digit = '7';
final int MAX = 45;
```

**LISTING 2.5**

```
//************************************************************************
// PianoKeys.java      Author: Lewis/Loftus
//
// Demonstrates the declaration, initialization, and use of an
// integer variable.
//************************************************************************

public class PianoKeys
{
    //------------------------------------------------------------
    // Prints the number of keys on a piano.
    //------------------------------------------------------------
    public static void main (String[] args)
    {
        int keys = 88;
        System.out.println ("A piano has " + keys + " keys.");
    }
}
```

**OUTPUT**

```
A piano has 88 keys.
```

In the PianoKeys program, two pieces of information are used in the call to the println method. The first is a string, and the second is the variable keys. When a variable is referenced, the value currently stored in it is used. Therefore, when the call to println is executed, the value of keys, which is 88, is obtained. Because that value is an integer, it is automatically converted to a string and concatenated with the initial string. The concatenated string is passed to println and printed.

A variable declaration can have multiple variables of the same type declared on one line. Each variable on the line can be declared with or without an initializing value. For example:

```
int count, minimum = 0, result;
```

### The Assignment Statement

Let’s examine a program that changes the value of a variable. Listing 2.6 shows a program called Geometry. This program first declares an integer variable called sides and initializes it to 7. It then prints out the current value of sides.

The next line in main changes the value stored in the variable sides:

```
sides = 10;
```

This is called an assignment statement because it assigns a value to a variable. When executed, the expression on the right-hand side of the assignment operator (=) is evaluated, and the result is stored in the memory location indicated by the variable on the left-hand side. In this example, the expression is simply a number, 10. We discuss expressions that are more involved than this in the next section.

**LISTING 2.6**

```
//***************************************************************************
// Geometry.java      Author: Lewis/Loftus
//
// Demonstrates the use of an assignment statement to change the
// value stored in a variable.
//***************************************************************************

public class Geometry
{
    //-------------------------------------------------------------
    // Prints the number of sides of several geometric shapes.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        int sides = 7;  // declaration with initialization
        System.out.println ("A heptagon has " + sides + " sides.");

        sides = 10;  // assignment statement
        System.out.println ("A decagon has " + sides + " sides.");

        sides = 12;
        System.out.println ("A dodecagon has " + sides + " sides.");
    }
}
```

**OUTPUT**

```
A heptagon has 7 sides.
A decagon has 10 sides.
A dodecagon has 12 sides.
```

> **KEY CONCEPT**  
> Accessing data leaves it intact in memory, but an assignment statement overwrites the old data.

A variable can store only one value of its declared type. A new value overwrites the old one. In this case, when the value 10 is assigned to sides, the original value 7 is overwritten and lost forever, as follows:

After initialization: sides 7

After first assignment: sides 10

### Basic Assignment

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_96_0.png)

The basic assignment statement uses the assignment operator (=) to store the result of the Expression into the specified Identifier, usually a variable.

Examples:

```
total = 57;
count = count + 1;
value = (min / 2) * lastValue;
```

When a reference is made to a variable, such as when it is printed, the value of the variable is not changed. This is the nature of computer memory: Accessing (reading) data leaves the values in memory intact, but writing data replaces the old data with the new.

The Java language is strongly typed, meaning that we are not allowed to assign a value to a variable that is inconsistent with its declared type. Trying to combine incompatible types will generate an error when you attempt to compile the program. Therefore, the expression on the right-hand side of an assignment statement must evaluate to a value compatible with the type of the variable on the left-hand side.

> **KEY CONCEPT**  
> We cannot assign a value of one type to a variable of an incompatible type.

### Constants

Sometimes we use data that is constant throughout a program. For instance, we might write a program that deals with a theater that can hold no more than 427 people. It is often helpful to give a constant value a name, such as MAX_OCCUPANCY, instead of using a literal value, such as 427, throughout the code. The purpose and meaning of literal values such as 427 is often confusing to someone reading the code. By giving the value a name, you help explain its role in the program.

Constants are identifiers and are similar to variables except that they hold a particular value for the duration of their existence. Constants are, to use the English meaning of the words, not variable. Their value doesn’t change.

> **KEY CONCEPT**  
> Constants hold a particular value for the duration of their existence.

In Java, if you precede a declaration with the reserved word final, the identifier is made a constant. By convention, uppercase letters are used when naming constants to distinguish them from regular variables, and individual words are
