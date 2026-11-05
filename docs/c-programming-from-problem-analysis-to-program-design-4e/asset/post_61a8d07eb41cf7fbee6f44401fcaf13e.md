
static and dynamic Web pages and how HTML and Web server controls differ. Master pages and Cascading Style Sheets are introduced. Also included in Chapter 15 is an introduction to mobile applications that can be viewed with small smart devices such as the Windows Phone. Chapter 15 illustrates how validation controls can be used to check users' input values and shows how the ADO.NET classes, introduced in Chapter 14, can also be used with Web applications to access database records.

Appendix A presents suggestions for customizing the appearance and behavior of the Integrated Development Environment (IDE). Appendix B discusses the Code Editor features of Visual Studio. Code snippets and refactoring are described. These new features improve programmer productivity by reducing the number of keystrokes required to enter program statements. This appendix also illustrates developing applications visually using class diagrams. Appendix C lists the Unicode and ASCII (American Standard Code for Information Interchange) character sets. Appendix D shows the precedence of the C# operators and Appendix E lists the C# keywords.

## Features

Every chapter in this book includes the following features. These features are both conducive to learning in the classroom and enable you to learn the material at your own pace.

- Multi-color interior design shows accurate C# code and related comments.
- Learning objectives offer an outline of the concepts discussed in detail in the chapter.
- Hundreds of visual diagrams throughout the text illustrate difficult concepts.
- Syntax boxes show the general form for different types of statements.
- Numbered examples illustrate the key concepts with their relevant code, and the code is often followed by a sample run. An explanation follows that describes the functions of the most difficult lines of code.
- Notes highlight important facts about the concepts introduced in the chapter.
- Numerous tables are included that describe and summarize information compactly for easy viewing.
- A Coding Standards section provides a summary of acceptable conventions or guidelines pertaining to the chapter's topic. These coding/programming guidelines help ensure consistency and reduce the number of bugs and errors entered into programming projects.
- Internet sites listed including tutorials that can be used to enhance concepts are presented in the Resources section.
- Programming Examples are complete programs featured at the end of the chapter. The examples contain the distinct stages of preparing a problem specification, analyzing the problem, designing the solution, and coding the solution.
- Quick Reviews offer a summary of the concepts covered in the chapter.
- Exercises further reinforce learning and ensure that students have, in fact, absorbed the material. Both objective and subjective types of questions are included at the end of each chapter.
- Programming Exercises challenge students to write C# programs with a specified outcome.
- The glossary at the end of the book lists nearly four-hundred key terms in alphabetical order along with definitions for easy reference. Throughout this text the terms set in bold indicate that they are defined in the glossary.

From beginning to end, the concepts are introduced at a pace that is conducive to learning. The writing style of this book is simple and straightforward, and it parallels the teaching style of a classroom. The concepts introduced are described using examples and small programs.

The chapters have two types of programs. The first type includes small programs that are part of the numbered examples and are used to explain key concepts. This book also features numerous case studies called Programming Examples. These Programming Examples are placed at the end of the chapters to pull together many of the concepts presented throughout the chapter. The programs are designed to be methodical and workable. Each Programming Example starts with a Problem Analysis and is then followed by the Algorithm Design. Every step of the algorithm is then coded in C#. In addition to teaching problem-solving techniques, these detailed programs show the user how to implement concepts in an actual C# program. Students are encouraged to study the Programming Examples very carefully in order to learn C# effectively.

All source code and solutions have been written, compiled, and tested by quality assurance with Visual Studio Professional 2012.

Microsoft® Visual C#® can be packaged with this text. Please contact your Course Technology Sales Representative for more information.

## Features of the Book

Numerous visual diagrams throughout the text illustrate difficult concepts. Updated screen shots of what readers see in Visual Studio are also included throughout the book.

![](img/36e48639a06772bcb0fa1ea2525b33a3_29_0.png)

FIGURE 8-2 Two-dimensional calories array

Data is not really stored in memory in a table such as this. Values are stored side by side in contiguous memory locations using a row major format.

The identifier calories contains a reference to calories[0, 0]. The Length property can be used with multidimensional arrays to get the total number of elements in all dimensions. The following statement displays 21:

`Console.WriteLine(calories.Length); // Length returns number of cells.`

Another useful member of the Array class is the GetLength() method. It can be called to return the number of rows or columns. Arrays are also zero based for specifying their dimensions. With a two-dimensional array, the first dimension (indexed by 0) represents the number of rows and the second dimension (indexed by 1) represents the number of columns. GetLength(0) returns the number of rows and GetLength(1) returns the number of columns, as shown in Example 8-2.

### EXAMPLE 8-2

```text
Console.WriteLine(calories.GetLength(0)); // Displays 3 (rows)
Console.WriteLine(calories.GetLength(1)); // Displays 7 (columns)
Console.WriteLine(calories.Rank);        // Displays 2 (dimensions)
```

**NOTE** The property Rank returns the number of dimensions of the array.

Multi-color interior design shows accurate C# code and related comments. Throughout the book, keywords are shown in blue and comments appear in green.

works for tests of equality. The switch statement could be used to replace the if...else program statements shown in Example 5–2.

### Switch Selection Statements

The **switch statement** is considered a multiple selection structure. It also goes by the name **case statement**. The switch statement allows you to perform a large number of alternatives based on the value of a single variable. This variable or expression must evaluate to an integral or string value. It cannot be used with a double, decimal, or float. But it is appropriate for short, int, long, char, and string data types. The general format of the switch statement follows:

```text
switch (expression)
{
    case value1: statement(s);
                  break;
    case value2: statement(s);
                  break;
    ...
    case valueN: statement(s);
                  break;
    [default:    statement(s);
                  break;]
}
```

With the switch statement, the expression is sometimes called the **selector**. Its value determines, or selects, which of the cases will be executed. When a switch statement is executed, the expression is evaluated and its result is compared to each case’s value.

The case value must be a constant literal of the same type as the expression. You cannot use a variable in the value spot for the case. Nor can you use an expression, such as x < 22, in the value spot for case. If the expression is a string variable, the value is enclosed in double quotes. If the expression is a char variable, the value is enclosed in single quotes. For integers, the number is typed without any special surrounding symbols.

The comparison to the case values is from top to bottom. The first case value that matches the expression results in that case’s statements being executed. If no match is made, the statements associated with default are executed. Default is optional, but usually it is a good idea to include one. The default statements are only executed when there is no match of any of the case values.

The curly braces are required with a switch statement. That is different from an if statement in which they are only required when more than one statement makes up the

![](img/36e48639a06772bcb0fa1ea2525b33a3_30_0.png)
