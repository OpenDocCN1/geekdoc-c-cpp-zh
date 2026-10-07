
# Chapter 10 More on Variables and Data Types

Note that the inherited alloc method wasn't overridden here; instead, you defined your owner allocator method. Your method will take advantage of the inherited alloc method. Place this code in your Fraction.m implementation file:

```objc
static int gCounter;
```

```objc
@implementation Fraction

+(Fraction *) allocF
{
    extern int gCounter;
    ++gCounter;

    return [Fraction alloc];
}
```

```objc
(int) count
{
    extern int gCounter;

    return gCounter;
}
// other methods from Fraction class go here

end
```

> Note
> it's not considered good programming practice to override alloc, as this method deals with the physical allocation of the memory. You don't have to get involved at that level.

The static declaration of gCounter makes it accessible to any method defined in the implementation section, yet it does not make it accessible from outside the file. The alloc method simply increments the gCounter variable and then uses the alloc method to create a new Fraction, returning the value of the counter, isolating its direct access from the user.
Recall that the extern declarations are not required in the two methods because gCounter is defined within the file. It helps the reader understand that a variable defined outside the method is being accessed. The g prefix for the variable name also serves the same purpose for the reader; for that reason, most programmers do not include the extern declarations. Program 10.2 tests the new methods.

# Program 10.2

```objc
#import "Fraction.h"
```

```objc
int main (int argc, char *argv[])
{
    NSAutleasePool * pool = [[NSAutleasePool alloc] init];
```

Fraction *a, *b, *c;
NSLog("Fractions allocated: %i", [Fraction count]);

```objc
a [[Fraction allocF] init];
b [[Fraction allocF] init];
c [[Fraction allocF] init];
```

NSLog("Fractions allocated: %i", [Fraction count]);
[a release];
[b release];
[c release];

```objc
[pool drain];
return 0;
```

# Program 10.2 Output

Fractions allocated: 0
Fractions allocated: 3

When the program begins execution, the value of qCounter is automatically set to 0 (recall that you can override the inherited class initialize method if you want to perform any special initialization of the class as a whole, such as setting the value of other state variables to some nonzero values). After allocating (and then initializing) 3 Fractions using the allocF method, the counter method retrieves the counter variable, which is correctly set to 3. You could also add a setter method to the class if you wanted to reset or set it to a particular value. You don't need that for this application, though.

# Enumerated Data Types

The Objective-C language enables you to specify a range of values that can be assigned to a variable. An enumerated data type is initiated by the keyword enum. Immediately following the keyword is the name of the enumerated data type, followed by a list of identifiers (enclosed in a set of curly braces) that define the possible values that can be assigned to the type. For example, the following statement defines a type flag:

```objc
enum flag { false, true };
```

In this theory, this type can be assigned the values true and false inside the program, and no other values. Unfortunately, the Objective-C compiler does not generate warning messages if this rule is violated.

To declare a variable to of type enum, again use the keyword enum, followed by the enumerated name, and the variable list. The following statement defines the two variables endData and matchFound to be of type flag:

```objc
enum flag endData, matchFound;
```

The only values (in theory, that is) that can be assigned to these variables are the names true and false. Thus, statements such as

```objc
endOfData true;
```

and

```objc
if ( matchFound false )
```

...

are valid.
If you want to have a specific integer value associated with an enumeration identifier, the integer can be assigned to the identifier when the data type is defined. Enumeration identifiers that subsequently appear in the list are assigned sequential integer values begin- with the specified integer value plus one.

In the following definition, an enumerated data type, direction, is defined with the values up, down, left, right:

```objc
enum direction { up, down, left = 10, right };
```

The compiler assigns the value 0 to up because it appears first in the list, assigns 1 to down because it appears next, assigns 10 to left because it is explicitly assigned this value, and 11 to right because it is the incremented value of the preceding enum in the list.

Enumeration identifiers share the same value. For example, in

```objc
enum boolean { no = 0, false 0, yes 1, true 1 };
```

assigning either the value no or false to a boolean variable assigns the value 0; assigning either yes or true assigns the value 1

Another example of an enumerated data type definition, the following defines the type month, with permissible values that can be assigned to a variable of this type being the number of months of the year:

```objc
enum month { january = 1, february, march, april, may, june, july, august, september, october, december };
```

The Objective-C compiler treats enumeration identifiers as integer constants. If your program contains these two lines, the value 2 would be assigned to thisMonth (and not the name february):

...

```objc
thisMonth = february;
```

Program 10.3 shows a simple program using enumerated types. The program reads a month number and then uses switch statement to see which month was entered.

```objc
#import <Foundation.h>

int main(int argc, char *argv[]) {
    NSAutleasePool *pool = [[NSAutleasePool alloc] init];

    enum month { january = 1, february, march, april, may, june, july, august, september, october, december };
    enum month amon;
    int days;

    NSLog("Enter month number: ");
    amon = (enum month)argv[1];

    switch (amon) {
        case january:
            days = 31;
            break;
        case february:
            days = 28;
            break;
        case march:
            days = 31;
            break;
        case april:
            days = 30;
            break;
        case may:
            days = 31;
            break;
        case june:
            days = 30;
            break;
        case july:
            days = 31;
            break;
        case august:
            days = 31;
            break;
        case september:
            days = 30;
            break;
        case october:
            days = 31;
            break;
        case november:
            days = 30;
            break;
        case december:
            days = 31;
            break;
        default:
            NSLog("bad month");
            days = 0;
            break;
    }

    if (days != 0) {
        NSLog("Number of days is %i", days);

        if (amon == february) {
            NSLog("or 29 if it's a leap year");
        }
    }

    [pool drain];
    return 0;
}
```

# Program 10.3 Output

Enter month: 5
Number of days is 31

# Program 10.3 Output (Rerun)

Enter month: 2
Number of days is 28
or 29 if it's a leap year

You can explicitly assign an integer value to an enumerated data type variable; you should do this using the type cast operator. Therefore, if monthValue were an integer variable that had the value 6, for example, this would be:

```objc
lastMonth = (enum month)(monthValue - 1);
```

If you don't use the type cast operator, the compiler (unfortunately) will complain about it.

When using programs with enumerated types, try not to rely on the fact that the enumerated values are treated as integers. Instead, treat them as distinct data types. The enumerated data type gives you a way to associate a symbolic name with an integer number. If you subsequently change the value of the enumeration, you must change it in the place.

# The typedef Statement

Objective-C provides a capability that enables the programmer to assign an alternative name to a data type.This is known as typedef. The following statement defines the name Counter to be equivalent to the Objective-C data type int:
typedef int Counter;
