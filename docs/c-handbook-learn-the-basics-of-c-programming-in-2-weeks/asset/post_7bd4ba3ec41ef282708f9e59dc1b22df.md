
Each time a nested block starts, a new level of indentation gets pushed on the stack. The *indent token* is then inserted into the stream, which is eventually passed on to the parser. It is not possible to have more than a single indent token in succession.

In the event that a line is seen with a smaller level of indentation, the values start popping from the stack until one of them gets on top. This is equivalent to the new level of indentation. In case there is nothing found, a syntax error is generated. For every value popped, there is a *dedent token*. It is possible to have multiple dedent tokens in succession. At the end of every source code, there are dedent tokens generated for the level of indentation that is left at the stack. This continues to occur until there is 0 left.

## Multiline Statements

When you end a statement, you can either use a new line or a continuation symbol ( \ ) if you want to indicate that the line needs to continue. To help you understand this concept further, consider the following example:

```
total = first_item + \
    second_item + \
    third_item
```

There is no need for you to use the continuation symbol when you write statements that are contained within brackets, such as { }, ( ), and [ ]. For instance, if you wish to display the months in a year, you may simply write:

```
year = [ 'January' , 'February' , 'March' , 'April' , 'May' , 'June' , 'July' , 'August' ,
'September' , 'October' , 'November' , 'December' ]
```

You are allowed to write multiple statements on a single line or create multiple groups as suites. When it comes to writing multiple statements, keep in mind that the inclusion of the semicolon ( ; ) is crucial. The semicolon allows you to write as many statements as possible, as long as they do not start a new block of code. Consider the following example:

```
import sys ; y = 'bar' ; sys.stdout.write ( y + '\n' )
```

So what are suites exactly? Well, they are groups of statements that consist of blocks of code. Compound or complex statements, such as *if*, *while*, *def*, and *class* require a suite and a header line.

So what are header lines? They begin statements with a keyword and end them with a colon (:). Also, they are followed by one or more lines that make up a suite. Consider the following example:

```
if expression :
    suite
elif expression :
    suite
else :
    suite
```

## Quotation

As a programmer, you are allowed to use a single quote ( ' ' ), double quote ( " " ), and a triple quote ( ''' or """ ) when you denote string literals. Then again, see to it that you use the same type of quotes at the start and end of your string. Typically, triple quotes are used to span strings across multiple lines. Take a look at the following example:

```
paragraph = """ You are reading an example of a paragraph that consists multiple lines
and sentences. You are an excellent programmer. """
```

## Comments

When it comes to comments, you should use the hash symbol ( # ) to start them. However, this hash symbol should not be within a string literal. Also, the characters after it towards the end of the line should be included in the comment. In Python, comments are not recognized by the interpreter. To help you understand this concept further, take a look at the following example:

```
# This is the first comment
print " Monty Python’s Flying Circus is a British sketch comedy series. " ;
# This is the second comment
```

If you run the example given above, you will obtain the following output:

```
Monty Python’s Flying Circus is a British sketch comedy series.
```

You can also write another comment after an expression or a statement, such as in the following:

```
name = "Wendy" # This is a sample comment
```

If you want to comment on multiple lines, you may do so as well. For example:

```
# This is a sample comment.
# This one is also a comment.
# This is another comment.
# This comment is written by Wendy.
```

## *Blank Lines*

These lines are not recognized in the Python programming language. With this being said, they are pretty much like comments. They contain whitespaces and even comments. You have to use empty lines to terminate multiline statements in an interactive interpreter session.

## Chapter 3: Data Types

In Python, input data are sorted according to different categories. The primary purpose of sorting is to help programmers like you in processing information more efficiently. Such categories function as data storage locations that you can access whenever you run the Python platform.

### Variables

Variables contain values that have been specifically allocated to them. If you are working on complex codes for applications, you may want to store your information in these variables. Do not worry because you can access them anytime you need them. You can even use them to ensure that the information you gather from your end users stay safe and secured.

### Numeric Types

Numbers in the Python programming language are different from the numbers you use to solve problems in Algebra. In Mathematics, adding .0 at the end of a number practically means nothing. It does not make any difference to its value. For instance, 3 and 3.0 are the same.

In Python, however, 3 and 3.0 are different numbers. Before the program processes it, it has to undergo certain data processing methods. As a programmer, you have to learn about the different numeric types.

### Integers

All whole numbers are integers. Numbers that contain a decimal point are not whole numbers; therefore, 3 is a whole number while 3.0 is not. Integers in Python are characterized by the data type *int*.

Take note that integers have capacity limitations. You will generate an error if you try to process a value beyond the allowed limits. Integers typically process numbers between -9,223,372,036,854 and 9,223,372,036,854.

There are interesting features that come with the *int* variable. For instance, base 2 only uses 0 and 1, base 8 uses numbers from 0 to 7, base 10 has similar properties with the decimal system and base 16 uses the letters A to F and the numbers 0 to 9 as digits.

### Floating Point Values

Any number that contains a decimal point is considered as a floating point value in Python. It does not matter if the number after the decimal point is 0 or not. 3.0, 1.5, and 11.4, for example, are all floating point values. They are stored in the float data type. One huge advantage of floating point values over integers is that they have bigger storage spaces; hence, they are capable of storing very small or large values.

Then again, you should not think that they have an unlimited storage space. There is still a limitation. Nevertheless, they can contain as little as ±2.2250738585072014 × 10⁻³⁰⁸ and as much as 1.7976931348623157 × 10⁻³⁰⁸. There are a couple of ways to allocate values with the use of floating point values. First, you can directly assign them. Second, you can use a scientific notation. Keep in mind that negative exponents produce fraction equivalents.

### Complex Numbers

These numbers consist of real numbers and imaginary numbers combined. Usually, they are used in dynamic systems, quantum mechanics, computer graphics, electrical engineering and fluid dynamics. Complex numbers can be processed in Python and a few other programming languages.

### ***Boolean Values***

These are the two constant objects *True* and *False*. They represent truth values. When used in a numeric context, they function as 0 and 1. You can use the function *bool* to assign a value to a Boolean if such value may be interpreted as a truth value.

### ***Strings***

They are groups of characters that are connected with double quotation marks. Consider the following example:

```
`TheString = " Python got its name from a popular comedy show. "`
```

As you can see in the sample code shown above, the phrase *Python got its name from a popular comedy show.* is assigned to the variable *TheString*.

Computers cannot understand letters, only numbers. So when you write a program, Python reads and interprets it based on the numbers that represent its letters. For example, in the American Standard Code for Information Interchange (ASCII), the number 65 represents the letter A. So if you type in

```
`ord ( " A " )`
```

you will get an output of
