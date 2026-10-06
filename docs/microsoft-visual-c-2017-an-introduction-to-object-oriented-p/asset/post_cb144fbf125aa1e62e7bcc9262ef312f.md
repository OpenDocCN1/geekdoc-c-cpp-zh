
# CHAPTER 1 A First Program Using C#

One way to compile a program from Visual Studio is to select Build the menu bar and select Build Solution from the drop-down menu. As an alternative, you can press Ctrl + Shift + B. You can also select Debug from the menu bar, and then click Start Without Debugging. The advantage of the later option is that the program will be compiled if there are no syntax errors and then execute to see the output.

# What to Do If You Receive a Programming Language Error Message in the IDE

If you receive a syntax error in a program in the IDE, you receive a programming language error message. For example, in Figure 1-13, WriteLine is spelled incorrectly because it uses a lowercase w. The error message displayed at the bottom is: 'writeLine does not exist in the current context.' If you cannot read the entire message on your screen, you can adjust the size of the window. The position is given (project, file, and line number), and as additional visual aids, a lightbulb appears to the left of the error, and a wavy underline emphasizes the unrecognized definition. When you fix the problem and compile the program again, the error, wavy line, and lightbulb are eliminated.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_54_0.png)

Figure 1-13 Error message generated when WriteLine is mistyped in the ThreeLinesOutput program compiled in the IDE

# Compiling and Executing a C# Program

In the lower left corner of Figure 1-13 you can see a code CS0103 next to the generated error message. You can search the Web for this and discover its general meaning. However, usually sufficient explanation is provided in Visual Studio, and a web search is unnecessary.

# What to Do When the Program Compiles Successfully in the IDE

If you receive no error messages after compiling the code, then the program compiled successfully, and you can run the program. Select **Debug** from the menu bar, and then select **Start Without Debugging**. The output appears, as you saw in Figure 1-6 earlier in this chapter.

# Noticing the Differences Between the Programs in the Text Editor and the IDE

There are a few differences between the ThreeLinesOutput programs in Figures 1-8 and 1-12. Specifically, the Visual Studio version in Figure 1-12 contains the extra components that are highlighted in Figure 1-14.

- **Five using statements at the top of the file.** Visual Studio automatically provides you with several commonly needed statements. In this case, you could delete all five statements from the Visual Studio version of the program, and the program would still run correctly. (The only statement you need to retain is the `using System.Console;` which allows you to use `WriteLine()` without qualification.) Conversely, you could add five additional `using` statements to the command-line version of the program, and it would also run correctly.
- **A namespace declaration and its opening and closing braces.** You already know that # uses built-in namespaces as System and others that are automatically listed at the top of the Visual Studio version of the program. C# also allows you to create your own namespaces; Visual Studio assumes that you will want to create one name you are using assigned to the project. In this case, you could remove the namespace declaration from the Visual Studio version of the program, or you could add one to the command-line version of the program. In both cases, the programs would still run correctly.
- **The class name Program.** Visual Studio assumes that you want to avoid confusion by having different names for your namespace and the class contained within it, so it assigns the generic name Program to the class that contains the Main() method. You could change this name to match the namespace identifier, ThreeLinesOutput, or use any other identifier, and the program would still work correctly. In the Notepad version of the program, you could change the class name to Program or any other identifier, and the program would also work.
- **The words string args between the parentheses of the Main() method header.** C# allows a program's Main() method header to be written in several ways. For example, you can include the words string[] args between the method's parameters, or you can omit them. The square brackets indicate an array, as you will learn when studying arrays later in this book. You could write the extra args in either the Notepad or Visual Studio version of the program, and the Main() method would still work correctly.

In summary, the Visual Studio version of the ThreeLinesOutput provides everything you need to run the program and saves you as much typing as possible in case you want to include additional options. The command-line and Visual Studio versions of the program function identically.

| Notepad version of the program | Visual Studio version of the program |
| :--- | :--- |
| using static System.Console; | using System; |
| | using System.Collections.Generic; |
| | using System.Linq; |
| | using System.Text; |
| | using System.Threading.Tasks; |
| | using static System.Console; |
| namespace ThreeLinesOutput | |
| class ThreeLinesOutput | class Program |
| static void Main() { | static void Main(string[] args) { |
| { WriteLine("Line one"); | { WriteLine("Line one"); |
| WriteLine("Line two"); | WriteLine("Line two"); |
| WriteLine("Line three"); | WriteLine("Line three"); |
| } } | } |

**Figure 1-14** Comparing the command line and Visual Studio versions of ThreeLinesOutput

# Deciding Which Environment to Use

When you write, compile, and execute a C# program, you can either use a text editor with the command line, or you can use the IDE. You would never need to use both. You might prefer using an editor you are already familiar with (such as Notepad) because only two files are generated.

On the other hand, the IDE provides many useful features, such as automatic statement completion. For example, if you type `u`, a list of choices including using is displayed and you can click it instead of typing it. Similarly, if you use `s`, then a list of choices is displayed.

Additionally, in the IDE, words are displayed using different colors based on their category; for example, one color is used for C#-reserved words and a different color for literal strings. It is also easier to correct many errors using the IDE. When compiler errors or warnings are issued, you can double-click the message, and the cursor jumps to the location in the code where the error was detected. Another advantage to the IDE is if you use another programming language in Visual Studio (C++ or Visual Basic), the environment will already be familiar to you. The C# language works the same no matter method you use to compile your programs. Everything you learn in the next chapters about input, output, decision making, loops, and arrays is correct in both environments. You can use just one or compile some programs in each environment as the mood strikes you. You can also mix and match techniques you prefer. For example, you can use an editor you like to compose your programs, paste them into the IDE to execute them. Although any program can be written using either compilation technique, when you write GUI applications using existing objects such as buttons and labels, you will find that the extensive amount of code automatically generated by the IDE is very helpful.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_57_0.png)

# TWO TRUTHS & A LIE
Compiling and Executing a C# Program

- After you write and save a program, you must compile it into intermediate language, and then the C# just in time (JIT) compiler must translate the intermediate code into executable code.
- You can compile and execute a C# program from the command line or within the Integrated Development Environment (IDE) that comes with Visual Studio.
- Many programmers prefer to compile their programs from the command line because it provides features such as color-coded keywords and automatic statement completion.

> The false statement is #3. Programmers who prefer the command line prefer its simplicity. Programmers who prefer the Visual Studio IDE prefer keywords and automatic statement completion.
