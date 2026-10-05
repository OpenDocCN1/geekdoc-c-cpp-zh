
1. In the StructsAndEnums project, display the Date.cs file in the Code and Text Editor window.

2. Add the following method to the Date structure. This method moves the date in the structure forward by one month. If, after advancing the month, the value of the month field has moved beyond December, the code resets the month to January and advances the value of the year field by 1.

Click here to view code image

```
struct Date
{
    public void AdvanceMonth()
    {
        this.month++;
        if (this.month == Month.December + 1)
        {
            this.month = Month.January;
            this.year++;
        }
    }
}
```

3. Display the Program.cs file in the Code and Text Editor window.

4. In the doWork method, comment out the first two uncommented statements that create and display the value of the defaultDate variable.

5. Add the following code to show in the end of the doWork method. This code creates a copy of the weddingAnniversary variable called weddingAnniversaryCopy and prints out the value of this new variable.

Click here to view code image

```
static void doWork()
{
    Date weddingAnniversaryCopy = weddingAnniversary;
    Console.WriteLine($"Value of copy is\n{weddingAnniversaryCopy}");
}
```

6. Add the following statements shown in bold to the end of the doWork method. These statements call the AdvanceMonth method of the weddingAnniversary variable and then display the value of the weddingAnniversary and weddingAnniversaryCopy variables:

Click here to view code image

```
static void doWork()
{
    weddingAnniversary.AdvanceMonth();
    Console.WriteLine($"New value of weddingAnniversary is {weddingAnniversary}");
    Console.WriteLine($"Value of copy is still {weddingAnniversaryCopy}");
}
```

7. On the Debug menu, select Start Without Debugging to build and run the application. Verify that the console window displays the following messages:

Click here to view code image

July 4 2021
Value of copy is July 4 2021
New value of weddingAnniversary is August 4 2021
Value of copy is still July 4 2021

If Date was a class, creating a copy would reference the same object in memory as the original instance. Changing the month in the original instance would therefore also change the date referenced through the copy. You'll verify this assertion in the following steps.

8. Press Enter and return to Visual Studio 2022.

9. Display the Date.cs file in the Code and Text Editor window.

10. Change the Date structure to a class, as shown in bold in the following example:

```
class Date
{
  ...
}
```

11. On the Debug menu, select Start Without Debugging to build and run the application again. Verify that the console window displays the following messages:

Click here to view code image

+   July 4 2021
Value of copy is July 4 2021
New value of weddingAnniversary is August 4 2021
Value of copy is still August 4 2021

The first three messages are the same as before. However, the fourth message shows that the value of the weddingAnniversaryCopy variable changed to August 4 2021.

12. Press Enter and return to Visual Studio 2022.

## Handling large structures

While most structures will be small in size, you can create structures that contain many fields and/or struct types. When you pass a variable of this type as a parameter to a method, the entire structure, including any child structures, will be copied to the stack. This can affect the performance of your applications if they do this often.

To counter this, pass the structure by reference using the ref modifier, as described in Chapter 8. However, be aware that changes made to the values held by fields in the structure will now be permanent; they are not made to a local copy. The following code shows an example:

Click here to view code image

```
struct BigStruct
{
  // Many, many fields here!
  ...
}
...
var myData = new BigStruct();
ProcessData(ref myData);
...
void ProcessData(ref BigStruct data)
{
  // data is a reference to myData, not a copy
}
```

## Summary

In this chapter, you saw how to create and use enumerations and structures. You learned some of the similarities and differences between a structure and a class, and you saw how to define constructors to initialize the fields in a structure. You also saw how to represent a structure as a string by overriding the ToString() method.

- If you want to continue to the next chapter, keep Visual Studio 2022 running and turn to Chapter 10, “Using arrays."
- If you want to exit Visual Studio 2022 now, on the File menu, select Exit. If you see a Save dialog, select Yes and save the project.

## Quick reference

| To | Do this |
| --- | --- |
| Declare an enumeration | Write the keyword `enum`, followed by the name of the type, followed by a pair of braces containing a comma-separated list of the enumeration literal names. For example: [Click here to view code image] <br> `enum Season { Spring, Summer, Fall, Winter }` |
| Declare an enumeration variable | Write the name of the enumeration on the left followed by the name of the variable, followed by a semicolon. For example: `Season currentSeason;` |
| Assign an enumeration variable to a value | Write the name of the enumeration literal in combination with the name of the enumeration to which it belongs. For example: [Click here to view code image] <br> `currentSeason = Season.Spring; // correct` <br> But note that: `currentSeason = Spring; // error` |
| Declare a structure type | Write the keyword `struct`, followed by the body of the structure (the constructors, methods, and fields). For example: [Click here to view code image] <br> `struct Time { public Time(int hh, int mm, int ss) { ... } private int hours, minutes, seconds; }` |
| Declare a structure variable | Write the name of the structure type, followed by the name of the variable, followed by a semicolon. For example:<br><br>`Time now;` |
| Initialize a structure variable to a value | Initialize the variable to a structure value created by calling the structure constructor. For example: [Click here to view code image] <br><br>`Time lunch = new Time(12, 30, 0);` |

# Chapter 10

# Using arrays

After completing this chapter, you will be able to:

- Declare array variables.
- Create an array instance.
- Populate an array with a set of data items and access those items.
- Copy arrays.
- Create and use multidimensional arrays.

You have already seen how to create and use variables of many different types. However, all the examples of variables you've seen so far have one thing in common: they hold information about a single item (an int, a float, a Circle, a Date, and so on). But what if you need to manipulate a set of items?

One solution is to create a variable for each item in the set, but this leads to some further questions:

- How many variables do you need?
- How should you name them?
- If you need to perform the same operation on each item in the set (such as increment each variable in a set), how would you avoid repetitive code?

Moreover, using a variable for separate items assumes you know how many items you need when you write the program. How often is this case? For example, if you're writing an application that reads and processes records from a database, how many records are in the database, and how likely is this number to change?

Arrays provide a mechanism that helps to solve these problems. An array is an unordered sequence of items. Unlike the fields in a structure or class, which can have different types, all the items in an array have the same type. Also, unlike fields in a structure or class which are accessed by name, the items in an array live in a contiguous block of memory and are accessed by using an index.

## Decl array variables

You declare an array variable by specifying the name of the element type, followed by a pair of square brackets, followed by the variable name. The square brackets signify that the variable is an array. For example, to declare an array of int variables named pins (for holding a set of personal identification numbers), you can write the following:

Click here to view code image

```
int[] pins; // Personal Identification Numbers
```

> Note
If you're a Microsoft Visual Basic programmer, notice that the declaration uses square brackets, not parentheses. If you're familiar with C and C++, also notice that the size of the array is not part of the declaration. Additionally, the square brackets must be placed before the variable name.

You are not restricted to using primitive types as array elements. You can also create arrays of structures, enumerations, and classes. For example, you can create an array of Date structures like this:

```
Date[] dates;
```

> Tip
It's often useful to give array variables plural names, such as places (where each element is a Place), people (where each element is a Person), or times (where each element is a Time).
