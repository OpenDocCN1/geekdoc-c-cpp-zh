
# C Example of Good String Declarations

```
/* Declare the string to have length of "constant+1".
Every other place in the program, "constant" rather
than "constant+1" is used. */
char name[ NAME_LENGTH + 1 ] = { 0 }; /* string of length NAME_LENGTH */
...
/* Example 1: Set the string to all 'A's using the constant,
NAME_LENGTH, as the number of 'A's that can be copied.
Note that NAME_LENGTH rather than NAME_LENGTH + 1 is used. */
for ( i = 0; i < NAME_LENGTH; i++ )
name[ i ] = 'A';
...
/* Example 2: Copy another string into the first string using
the constant as the maximum length that can be copied. */
strncpy( name, some_other_name, NAME_LENGTH );
```

The string is declared to be of length NAME_LENGTH +1.

Operations on the string using NAME_LENGTH here...

...and here.

If you don’t have a convention to handle this, you’ll sometimes declare the string to be of length NAME_LENGTH and have operations on it with NAME_LENGTH-1; at other times you’ll declare the string to be of length NAME_LENGTH+1 and have operations on it work with length NAME_LENGTH. Every time you use a string, you’ll have to remember which way you declared it.

When you use strings the same way every time, you don’t have to remember how you dealt with each string individually and you eliminate mistakes caused by forgetting the specifics of an individual string. Having a convention minimizes mental overload and programming errors.

Cross-Reference For more details on initializing data, see Section 10.3, "Guidelines for Initializing Variables."

# Initialize strings to null to avoid endless strings

C determines the end of a string by finding a null terminator, a byte set to 0 at the end of the string. No matter how long you think the string is, C doesn’t find the end of the string until it finds a 0 byte. If you forget to put a null at the end of the string, your string operations might not act the way you expect them to.

You can avoid endless strings in two ways. First, initialize arrays of characters to 0 when you declare them:

# C Example of a Good Declaration of a Character Array

```
char EventName[ MAX_NAME_LENGTH + 1 ] = { 0 };
```

Second, when you allocate strings dynamically, initialize them to 0 by using calloc() instead of malloc(). calloc() allocates memory and initializes it to 0. malloc() allocates memory without initializing it, so you take your chances when you use memory allocated by malloc().

**Use arrays of characters instead of pointers in C** If memory isn’t a constraint—and often it isn’t—declare all your string variables as arrays of characters. This helps to avoid pointer problems, and the compiler will give you more warnings when you do something wrong.

**Use `strncpy()` instead of `strcpy()` to avoid endless strings** String routines in C come in safe versions and dangerous versions. The more dangerous routines such as `strcpy()` and `strcat()` keep going until they run into a null terminator. Their safer companions, `strncpy()` and `strncmp()`, take a parameter for maximum length so that even if the strings go on forever, your function calls won’t.

# 12.5 Boolean Variables

It’s hard to misuse logical or boolean variables, and using them thoughtfully makes your program cleaner.

**Use boolean variables to document your program** Instead of merely testing a boolean expression, you can assign the expression to a variable that makes the implication of the test unmistakable. For example, in the next fragment, it’s not clear whether the purpose of the `if` test is to check for completion, for an error condition, or for something else:

```
Java Example of Boolean Test in Which the Purpose Is Unclear
if ( ( elementIndex < 0 ) || ( MAX_ELEMENTS < elementIndex ) ||
     ( elementIndex == lastElementIndex )
   ) {
   ...
}
```

In the next fragment, the use of boolean variables makes the purpose of the `if` test clearer:

```
Java Example of Boolean Test in Which the Purpose Is Clear
finished = ( ( elementIndex < 0 ) || ( MAX_ELEMENTS < elementIndex ) );
repeatedEntry = ( elementIndex == lastElementIndex );
if ( finished || repeatedEntry ) {
   ...
}
```

**Use boolean variables to simplify complicated tests** Often, when you have to code a complicated test, it takes several tries to get it right. When you later try to modify the test, it can be hard to understand what the test was doing in the first place. Logical variables can simplify the test. In the previous example, the program is really testing for two conditions: whether the routine is finished and whether it’s working on a repeated entry. By creating the boolean variables *finished* and *repeatedEntry*, you make the `if` test simpler: easier to read, less error prone, and easier to modify.

Here’s another example of a complicated test:

![](img/649c8eee28c38ca1e062691e45dc9883_338_0.png)

```
**Visual Basic Example of a Complicated Test**
```vb
If ( ( document.AtEndOfStream() ) And ( Not inputError ) ) And _
   ( ( MIN_LINES <= lineCount ) And ( lineCount <= MAX_LINES ) ) And _
   ( Not ErrorProcessing() ) Then
       do something or other
...
End If
```
```

The test in the example is fairly complicated but not uncommonly so. It places a heavy mental burden on the reader. My guess is that you won’t even try to understand the *if* test but will look at it and say, “I’ll figure it out later if I really need to.” Pay attention to that thought because that’s exactly the same thing other people do when they read your code and it contains tests like this.

Here’s a rewrite of the code with boolean variables added to simplify the test:

```
**Visual Basic Example of a Simplified Test**
```vb
allDataRead = ( document.AtEndOfStream() ) And ( Not inputError )
legalLineCount = ( MIN_LINES <= lineCount ) And ( lineCount <= MAX_LINES )
If ( allDataRead ) And ( legalLineCount ) And ( Not ErrorProcessing() ) Then
    do something or other
End If
```
```

> Here’s the simplified test.

This second version is simpler. My guess is that you’ll read the boolean expression in the *if* test without any difficulty.

***Create your own boolean type, if necessary***  Some languages, such as C++, Java, and Visual Basic have a predefined boolean type. Others, such as C, do not. In languages such as C, you can define your own boolean type. In C, you’d do it this way:

```
**C Example of Defining the *BOOLEAN* Type Using a Simple *typedef***
```c
typedef int BOOLEAN;
```
```

Or you could do it this way, which provides the added benefit of defining *true* and *false* at the same time:

```
**C Example of Defining the *Boolean* Type Using an Enum**
```c
enum Boolean {
    True=1,
    False=(!True)
};
```
```

Declaring variables to be *BOOLEAN* rather than *int* makes their intended use more obvious and makes your program a little more self-documenting.

# 12.6 Enumerated Types

An enumerated type is a type of data that allows each member of a class of objects to be described in English. Enumerated types are available in C++ and Visual Basic and are generally used when you know all the possible values of a variable and want to express them in words. Here are some examples of enumerated types in Visual Basic:

```
**Visual Basic Examples of Enumerated Types**
Public Enum Color
    Color_Red
    Color_Green
    Color_Blue
End Enum

Public Enum Country
    Country_China
    Country_England
    Country_France
    Country_Germany
    Country_India
    Country_Japan
    Country_Usa
End Enum

Public Enum Output
    Output_Screen
    Output_Printer
    Output_File
End Enum
```

Enumerated types are a powerful alternative to shopworn schemes in which you explicitly say, “1 stands for red, 2 stands for green, 3 stands for blue....” This ability suggests several guidelines for using enumerated types:

*Use enumerated types for readability* Instead of writing statements like

```
if chosenColor = 1
```

you can write more readable expressions like

```
if chosenColor = Color_Red
```

Anytime you see a numeric literal, ask whether it makes sense to replace it with an enumerated type.

Enumerated types are especially useful for defining routine parameters. Who knows what the parameters to this function call are?
