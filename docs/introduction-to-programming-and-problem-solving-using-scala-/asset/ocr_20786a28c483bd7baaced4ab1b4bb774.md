# Type Basics and Argument Passing 195

you have a syntax error it means your program is not valid for the language you are writing in, for our purposes that is Scala.

2. RUNTIME ERROR – Error that causes the program to crash while running.

3. LOGIC ERROR – Error that does not crash the code, but it causes it to produce the wrong answer.

Each of these deserves some discussion. We will also talk about how they compare to another and the way in which they impact programs.

When you are first learning to program, the errors that you likely run into the most are syntax errors. These can be simple typos or misspellings. They can also be complex like type mismatches or calling functions or methods with the wrong number of arguments. The common element that makes a syntax error is that it is discovered by the compiler when it is trying to translate the human written code into a format that is more computer friendly. Different programming languages do different amounts of checking for errors at compile time. This is often called STATIC CHECKING because it can be done without actually running the program.

Scala does a significant amount of static checking for errors.¹10 The way we have running our programs in the REPL or with scripts, the compile stage is not clearly separated from the running of the program. The Scala system is running a compiler in the background and executing the results of the compile. The syntax errors display a message like the following:

```
timing.scala:5: error: not found: value This
This line will not compile
```

one error found

They tell you the name of the file with a line number. Then they describe the error and show the line and where the line error occurred.

The second type of bug is a runtime error. This type of error occurs when everything is syntactically correct and the program compiles and runs. During during the run the error causes the program to crash. In Scala, a runtime error will produce a message that looks similar to the following:

```
java.lang.ArrayIndexOutOfBoundsException: -1
at Main$anon1.<init>(timing.scala:5)
at Main$main(timing.scala:1)
at Main$main(timing.scala)
```

This tells you what you wrote and then prints something called the code failed on line 5. The stack trace includes line numbers. The stack trace shows the line of code that was currently executing at the top, followed by the line that called that function, and so on. Sometimes the line is not in your code, but something you passed into a library call. You can look down the stack trace to find the first line that is in your code for guidance on what is causing the problem.

There are many different reasons why runtime errors happen, and it might be dependent on user input. So a runtime error might not be found running the program or

¹⁰The significant static checking of types was a major influence in the selection of Scala for this textbook. Other introductory languages, like Python, do significantly less static checking of programs.