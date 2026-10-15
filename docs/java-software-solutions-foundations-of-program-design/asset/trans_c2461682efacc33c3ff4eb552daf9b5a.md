

## LISTING 3.5

```
//************************************************************************
// CircleStats.java        Author: Lewis/Loftus
//
// Demonstrates the formatting of decimal values using the
// DecimalFormat class.
//************************************************************************

import java.util.Scanner;
import java.text.DecimalFormat;

public class CircleStats
{
    //-------------------------------------------------------------
    // Calculates the area and circumference of a circle given its
    // radius.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        int radius;
        double area, circumference;

        Scanner scan = new Scanner (System.in);

        System.out.print ("Enter the circle's radius: ");
        radius = scan.nextInt();

        area = Math.PI * Math.pow(radius, 2);
        circumference = 2 * Math.PI * radius;

        // Round the output to three decimal places
        DecimalFormat fmt = new DecimalFormat ("0.###");

        System.out.println ("The circle's area: " + fmt.format(area));
        System.out.println ("The circle's circumference: "
                           + fmt.format(circumference));
    }
}
```

## OUTPUT

Enter the circle's radius: 5
The circle's area: 78.54
The circle's circumference: 31.416

name. The values of id and name are inserted into the string, producing a result such as:

```
ID: 24036  Name: Larry Flagelhopper
```

The printf method was added to Java to mirror a similar function used in programs written in the C programming language. It makes it easier for a programmer to translate (or migrate) an existing C program into Java.

Older software that still has value is called a legacy system. Maintaining a legacy system is often a costly effort because, among other things, it is based on older technologies. But in many cases, maintaining a legacy system is still more cost effective than migrating it to new technology, such as writing it in a newer language. Adding the printf method is an attempt to make such migrations easier, and therefore less costly, by providing the same kind of output statement that C programmers have come to rely on.

However, using the printf method is not a particularly clean object-oriented solution to the problem of formatting output, so we avoid its use in this book.

> KEY CONCEPT
> The printf method was added to Java to support the migration of legacy systems.

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

- SR 3.25 Describe how you request a NumberFormat object for use within a program.
- SR 3.26 Suppose that in your program you have a double variable named cost. You want to output the value stored in cost formatted as the currency of the current locale.
  a. Write a code statement that declares and requests a NumberFormat object named moneyFormat that can be used to represent currency in the format of the current locale.
  b. Write a code statement that uses the moneyFormat object and prints the value of cost, formatted as the currency of the current locale.
  c. What would be the output from the statement you wrote in part (b) if the value in cost is 54.89 and your computer’s locale is set to the United States? What if your computer’s locale is set to the United Kingdom?
- SR 3.27 What are the steps to output a floating point value as a percentage using Java’s formatting classes?
- SR 3.28 Write code statements that prompt for and read in a double value from the user, and then print the result of taking the square root of the absolute value of the input value. Output the result to two decimal places.

## 3.7 Enumerated Types

Java provides the ability to define an enumerated type, which can then be used as the type of a variable when it is declared. An enumerated type establishes all possible values of a variable of that type by listing, or enumerating, them. The values are identifiers, and can be anything desired.

For example, the following declaration defines an enumerated type called Season, whose possible values are winter, spring, summer, and fall:

```
enum Season {winter, spring, summer, fall}
```

There is no limit to the number of values that you can list for an enumerated type. Once the type is defined, a variable can be declared of that type:

```
Season time;
```

> KEY CONCEPT
> Enumerated types are type-safe, ensuring that invalid values will not be used.

The variable time is now restricted in the values it can take on. It can hold one of the four Season values, but nothing else. Java enumerated types are considered to be type-safe, meaning that any attempt to use a value other than one of the enumerated values will result in a compile-time error.

The values are accessed through the name of the type. For example:

```
time = Season.spring;
```

Enumerated types can be quite helpful in situations in which you have a relatively small number of distinct values that a variable can assume. For example, suppose we wanted to represent the various letter grades a student could earn. We might declare the following enumerated type:

```
enum Grade {A, B, C, D, F}
```

Any initialized variable that holds a Grade is guaranteed to have one of those valid grades. That’s better than using a simple character or string variable to represent the grade, which could take on any value.

Suppose we also wanted to represent plus and minus grades, such as A– and B+. We couldn’t use A– or B+ as values, because they are not valid identifiers (the characters ‘-’ and ‘+’ cannot be part of an identifier in Java). However, the same values could be represented using the identifiers Aminus, Bplus, etc.

Internally, each value in an enumerated type is stored as an integer, which is referred to as its ordinal value. The first value in an enumerated type has an ordinal value of 0, the second one has an ordinal value of 1, the third one 2, and so on. The ordinal values are used internally only. You cannot assign a numeric value to an enumerated type, even if it corresponds to a valid ordinal value.

An enumerated type is a special kind of class, and the variables of an enumerated type are object variables. As such, there are a few methods associated with all enumerated types. The ordinal method returns the numeric value associated with a particular enumerated type value. The name method returns the name of the value, which is the same as the identifier that defines the value.

Listing 3.6 shows a program called IceCream that declares an enumerated type and exercises some of its methods. Because enumerated types are special types of classes, they are not defined within a method. They can be defined either at the class level (within the class but outside a method), as in this example, or at the outermost level.

We explore enumerated types further in Chapter 6.

## LISTING 3.6

```
//************************************************************************
// IceCream.java        Author: Lewis/Loftus
//
// Demonstrates the use of enumerated types.
//************************************************************************

public class IceCream
{
    enum Flavor {vanilla, chocolate, strawberry, fudgeRipple, coffee,
                rockyRoad, mintChocolateChip, cookieDough}

    //------------------------------------------------------------
    // Creates and uses variables of the Flavor type.
    //------------------------------------------------------------
    public static void main (String[] args)
    {
        Flavor cone1, cone2, cone3;

        cone1 = Flavor.rockyRoad;
        cone2 = Flavor.chocolate;

        System.out.println ("cone1 value: " + cone1);
        System.out.println ("cone1 ordinal: " + cone1.ordinal());
        System.out.println ("cone1 name: " + cone1.name());

        System.out.println ();
        System.out.println ("cone2 value: " + cone2);
        System.out.println ("cone2 ordinal: " + cone2.ordinal());
        System.out.println ("cone2 name: " + cone2.name());

