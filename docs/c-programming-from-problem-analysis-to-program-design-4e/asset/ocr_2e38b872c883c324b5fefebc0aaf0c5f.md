**Source code** consists of program statements written using a programming language, such as C#.

NOTE

Source code statements can be typed into the computer using an editor such as Notepad or an **integrated development environment (IDE)**, such as Visual Studio. IDEs include a number of useful development tools: IntelliSense (pop-up windows with completion options), debugging, color coding of different program sections, online help and documentation, and features for running the program.

You must follow the syntax of the language when you code the solution. Whether you speak English, Spanish, or another language, you are accustomed to following language **syntax**, or rules. For example, the syntax of the English language dictates that statements end with periods and include subjects and verbs. When you write in English, you are expected to follow those rules. When you write in the C# programming language, you are expected to follow the rule that every statement should end with a semicolon. It is at this third phase of the program development process (code the solution) that you must concern yourself with language syntax.

Many programmers use an **iterative approach** in the software development process. This means that you might find it necessary to go back to the design stage to make modifications. There might even be times when additional analysis is necessary. If you analyze and design thoroughly before attempting to code the solution, you usually develop a much better program that is easier to read and modify.

+   4. **Implement the code.** During this phase, the typed program statements (source code) are compiled to check for rule violations. Integrated development environments (IDEs) such as Visual Studio supply compilers within the development environment. The output of the compiler is a listing of the errors along with a brief description of the violation. Before the implementation can go forward, all the syntax errors must be corrected. When rule violations are eliminated, the source code is converted into the Microsoft **Intermediate Language (IL)**. All languages targeting the .NET (pronounced dot net) platform compile into an IL. The language that you will be using in this book, C#, is a language introduced as part of the .NET platform. Like C#, other languages, such as Java, compile code into an intermediate language. Java’s intermediate language is called **bytecode**. Intermediate languages facilitate the use of code that is more platform independent than other languages that compile straight into the machine language of the specific platform.

NOTE

If you are using the Visual Studio IDE, you might not be aware of the IL’s presence. You simply select options to compile, build, and execute the program to see the output results.