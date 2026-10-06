# Pseudocode

Recall from Chapter 1 that each programming language has strict rules, known as syntax, that the programmer must follow when writing a program. If the programmer writes code that violates these rules, a syntax error will result and the program cannot be compiled or executed. When this happens, the programmer has to locate the error and correct it.

Because small mistakes like misspelled words and forgotten punctuation characters can cause syntax errors, programmers must be mindful of such small details when writing code. For this reason, programmers find it helpful to write their programs in pseudocode (pseudone "due code") before they write it in the actual code of a programming language.

The word pseudocode means fake, so pseudocode is fake code. It is an informal language that has no syntax, and is not meant to be compiled or executed. Instead, programmers use pseudocode to create models, or "mock-ups" of programs. Because programmers do not have to worry about syntax errors while writing pseudocode, they can focus all of their attention on the program's design. A satisfactory design has been created with pseudocode, the pseudocode can be translated to actual code.

Here is an example of how you might write pseudocode for the paying program that we discussed earlier:

```
Display "Enter the number of hours the employee worked.
Input hours
Display "Enter the employee's hourly pay rate."
Input payRate
Set grossPay = hours * payRate
Display "The employee's gross pay is $, grossPay"
```

Each statement in the pseudocode represents an operation that can be performed in any high-level language. For example, all languages provide a way to display messages on the screen, read input that is typed on the keyboard, and perform mathematical calculations. For, don't worry about the details of this particular pseudocode program. As you progress through this chapter you will learn more about each of the statements that you see here.

> NOTE: As you read the examples in this book, keep in mind that pseudocode is not an actual programming language. It is a generic way to write the statements of an algorithm, without worrying about syntax rules. If you mistakenly write pseudocode into an editor for an actual programming language, such as Python or Visual Basic, errors will result.

# Flowcharts

Flowchart is another tool that programmers use to design programs. A flowchart is a diagram that graphically depicts the steps that take place in a program. Figure 2-2 shows how you might create a flowchart for the paying program.

Notice that there are three types of symbols in the flowchart: ovals, parallelograms, and rectangles. The ovals, which appear at the top and bottom of the flowchart, are