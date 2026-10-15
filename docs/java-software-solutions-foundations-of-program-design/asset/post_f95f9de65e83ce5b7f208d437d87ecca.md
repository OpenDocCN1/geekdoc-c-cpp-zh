
The System.out object also provides another service we can use: the print method. The difference between print and println is small but important. The println method prints the information sent to it, then moves to the beginning of the next line. The print method is similar to println, but does not advance to the next line when completed.

The program shown in Listing 2.1 is called Countdown, and it invokes both the print and println methods.

Carefully compare the output of the Countdown program, shown at the bottom of the program listing, to the program code. Note that the word Liftoff is printed on the same line as the first few words, even though it is printed using the println method. Remember that the println method moves to the beginning of the next line after the information passed to it has been printed.

## KEY CONCEPT

The print and println methods represent two services provided by the System.out object.

## LISTING 2.1

```
//************************************************************************
//  Countdown.java      Author: Lewis/Loftus
//
//  Demonstrates the difference between print and println.
//************************************************************************
public class Countdown
{
    //-------------------------------------------------------------
    //  Prints two lines of output representing a rocket countdown.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        System.out.print ("Three... ");
        System.out.print ("Two... ");
        System.out.print ("One... ");
        System.out.print ("Zero... ");
        System.out.println ("Liftoff!"); // appears on first output line
        System.out.println ("Houston, we have a problem.");
    }
}
```

## OUTPUT

Three... Two... One... Zero... Liftoff!
Houston, we have a problem.

## String Concatenation

A string literal cannot span multiple lines in a program. The following program statement is improper syntax and would produce an error when attempting to compile:

```
// The following statement will not compile
System.out.println ("The only stupid question is
the one that is not asked.");
```

When we want to print a string that is too long to fit on one line in a program, we can rely on string concatenation to append one string to the end of another. The string concatenation operator is the plus sign (+). The following expression concatenates one character string to another, producing one long string:

```
"The only stupid question is " + "the one that is not asked."
```

The program called Facts shown in Listing 2.2 contains several println statements. The first one prints a sentence that is somewhat long and will not fit on one line of the program. Since a character literal cannot span two lines in a program, we split the string into two and use string concatenation to append them. Therefore, the string concatenation operation in the first println statement results in one large string that is passed to the method to be printed.

Note that we don’t have to pass any information to the println method, as shown in the second line of the Facts program. This call does not print any visible characters, but it does move to the next line of output. So in this case calling println with no parameters has the effect of printing a blank line.

The last three calls to println in the Facts program demonstrate another interesting thing about string concatenation: Strings can be concatenated with numbers. Note that the numbers in those lines are not enclosed in double quotes and are therefore not character strings. In these cases, the number is automatically converted to a string, and then the two strings are concatenated.

Because we are printing particular values, we simply could have included the numeric value as part of the string literal, such as:

```
"Speed of ketchup: 40 km per year"
```

Digits are characters and can be included in strings as needed. We separate them in the Facts program to demonstrate the ability to concatenate a string and a number. This technique will be useful in upcoming examples.

As you can imagine, the + operator is also used for arithmetic addition. Therefore, what the + operator does depends on the types of data on which it

operates. If either or both of the operands of the + operator are strings, then string concatenation is performed.

The Addition program shown in Listing 2.3 demonstrates the distinction between string concatenation and arithmetic addition. The Addition program uses the + operator four times. In the first call to println, both + operations perform string concatenation, because the operators are executed left to right. The first operator concatenates the string with the first number (24), creating a larger string. Then that string is concatenated with the second number (45), creating an even larger string, which gets printed.

In the second call to println, we use parentheses to group the + operation with the two numeric operands. This forces that operation to happen first. Because both operands are numbers, the numbers are added in the arithmetic

## LISTING 2.3

```
//****************************************************************
// Addition.java      Author: Lewis/Loftus
//
// Demonstrates the difference between the addition and string
// concatenation operators.
//****************************************************************

public class Addition
{
    //-------------------------------------------------------------
    // Concatenates and adds two numbers and prints the results.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        System.out.println ("24 and 45 concatenated: " + 24 + 45);

        System.out.println ("24 and 45 added: " + (24 + 45));
    }
}
```

## OUTPUT

24 and 45 concatenated: 2445
24 and 45 added: 69

We revisit this type of situation later in this chapter when we formalize the precedence rules that define the order in which operators get evaluated.

## Escape Sequences

Because the double quotation character (") is used in the Java language to indicate the beginning and end of a string, we must use a special technique to print the quotation character. If we simply put it in a string ("""), the compiler gets confused because it thinks the second quotation character is the end of the string and doesn’t know what to do with the third one. This results in a compile-time error.

To overcome this problem, Java defines several escape sequences to represent special characters. An escape sequence begins with the backslash character (\), which indicates that the character or characters that follow should be interpreted in a special way. Figure 2.1 lists the Java escape sequences.

The program in Listing 2.4, called Roses, prints some text resembling a poem. It uses only one println statement to do so, despite the fact that the poem is several lines long. Note the escape sequences used throughout the string. The \n escape sequence forces the output to a new line, and the \t escape sequence represents a tab character. The \" escape sequence ensures that the quote character is treated as part of the string, not the termination of it, which enables it to be printed as part of the output.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_90_0.png)

> KEY CONCEPT
> An escape sequence can be used to represent a character that would otherwise cause compilation problems.

| Escape Sequence | Meaning |
|---|---|
| \b | backspace |
| \t | tab |
| \n | newline |
| \r | carriage return |
| \" | double quote |
| \' | single quote |
| \\ | backslash |

FIGURE 2.1 Java escape sequences

## LISTING 2.4

```
//************************************************************************
// Roses.java      Author: Lewis/Loftus
//
// Demonstrates the use of escape sequences.
//************************************************************************

public class Roses
{
    //-------------------------------------------------------------
    // Prints a poem (of sorts) on multiple lines.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        System.out.println ("Roses are red,\n\tViolets are blue,\n" +
            "Sugar is sweet,\n\tBut I have \"commitment issues\",\n\t" +
            "So I'd rather just be friends\n\tAt this point in our " +
            "relationship.");
    }
}
```

## OUTPUT

Roses are red,
    Violets are blue,
Sugar is sweet,
    But I have "commitment issues",
    So I'd rather just be friends
    At this point in our relationship.

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

- SR 2.1  What is a string literal?
- SR 2.2  What is the difference between the print and println methods?
- SR 2.3  What is a parameter?
- SR 2.4  What output is produced by the following code fragment?
    System.out.println ("One ");
    System.out.print ("Two ");
    System.out.println ("Three ");
