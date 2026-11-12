
## B.6 Debugging

Use breakpoints, single-stepping, watches, and temporary cout statements to find logic errors

No matter how much care you take in writing a program, it will contain errors that you need to track down. Fortunately, programs that are modular, clear, and well documented are generally amenable to debugging. Fail-safe techniques, which guard against certain errors and report them when they are encountered, are also a great aid in debugging.

Without a systematic approach, finding a small mistake in a large program can indeed be a difficult task. Many people have difficulty in debugging a program, perhaps because they believe that their program is really doing what it is supposed to do. For example, on receiving an execution-time error message at line 1098, a person might say, “That’s impossible. The statement at line 1098 was not even executed, because it is in the else clause, and I am positive that it was not executed.” However, the proper approach is either to trace the program’s execution by using available debugging facilities or to add cout statements that show which part of the if statement was executed. By doing so, you verify the value of the expression in the if statement. If the expression is 0, for example, when you expect it to be 1, the next step is to determine how it became 0.

How can you find the point in a program where something becomes other than what it should be? A typical Integrated Development Environment, or IDE, allows you to trace a program’s execution either by single-stepping through the statements in the program or by setting breakpoints at which execution will halt. You also can examine the contents of particular variables by either establishing watches or inserting temporary cout statements. The key to debugging is simply to use these techniques to tell you what is going on. This may sound pretty mundane, but the real trick is to use these debugging aids in an effective manner. After all, you do not simply put breakpoints, watches, and cout statements at random points in the program and have them report random information.

Systematically check a program's logic to determine where an error occurs

The main idea is systematically to locate the points of the program that cause the problem. A program’s logic implies that certain conditions should be true at various points in the program. If the program’s results differ from your expectations, an error occurs. To correct the error, you must find the first point in the program at which this difference is evident. By inserting either breakpoints and watches or cout statements at strategic locations of a program—such as at the entry and departure points of loops and functions—you can systematically isolate the error.

These diagnostic techniques should inform you whether things start going wrong before or after a given point in the program. Thus, after you run the program with an initial set of diagnostics, you should be able to trap the error between two points. For example, suppose that things are fine before you call method M, but that something is wrong by the time you call M. This kind of information allows you to focus your attention between these two points. You continue the process until eventually the search is limited to only a few statements. There is really no place in a program for an error to hide.

> Programming Tip: A statement of truth about some aspect of a program’s logic is known as an assertion. You can express an assertion either as a comment or by using the assert macro. By including assertions in your program, you facilitate the debugging process.

The ability to place breakpoints, watches, and cout statements in appropriate locations and to have them report appropriate information comes in part from thinking logically about the problem and in part from experience. Here are a few general guidelines.

### B.6.1 Debugging Functions and Methods

You should examine the values of the arguments passed to a function or method as at its beginning and end by using either watches or cout statements. Ideally, you should debug each major function or method separately before using it in your program.

### B.6.2 Debugging Loops

You should examine the values of key variables at the beginnings and ends of loops, as the comments in this example indicate:

```cpp
// Check values of start and stop before entering loop
for (index = start; index <= stop; index++)
{
    // Check values of index and key variables
    // at the beginning of iteration
    ...
    // Check values of index and key variables
    // at the end of iteration
}
// End for
// Check values of start and stop after exiting loop
```

### B.6.3 Debugging if Statements

Just before an if statement, you should examine the values of the variables within its expression. You can use either breakpoints or cout statements to determine which branch the if statement takes, as this example indicates:

```cpp
// Check variables within expression before executing if
if (expression)
{
    cout << "Condition is true (value of expression is 1).";
    ...
}
else
{
    cout << "Condition is false (value of expression is 0).";
    ...
} // end if
```

### B.6.4 Using cout Statements

Sometimes cout statements can be more convenient than watches. Such cout statements should report both the values of key variables and the location in the program at which the variables have those values. You can use a comment to label the location, as follows:

```cpp
// This is point A
cout << "At point A in the method computeResults:\n"
     << "x = " << x << ", y = " << y << endl;
```

Remember to either disable or remove these statements when your program finally works.

### B.6.5 Using Special Dump Functions

Often the variables whose values you wish to examine are arrays or other, more complex data structures. If so, you should write dump functions to display the data structures in a highly readable manner. You can easily move the single statement that calls each dump function from one point in the program to another as you track down an error. The time you spend on these functions often proves to be worthwhile, as you can call them repeatedly while debugging different parts of the program.

Hopefully, this discussion has conveyed the importance of the effective use of diagnostic aids in debugging. Even the best programmers have to spend some time debugging. Thus, to be a truly good programmer, you must be a good debugger.

## B.7 Testing

You can never test a program too much

Programs need to be tested to make sure that they correctly solve their current requirements. Good testing cannot happen without a plan. Software is complex, and determining whether it works correctly is not easy. Software testing is so important that some iterative development processes argue that tests should be developed before writing any code.

### B.7.1 Levels of Testing

Unit testing checks individual modules

Several levels of testing should take place. The first level of testing is called unit testing, and it happens on the individual modules. You should test individual methods first, and then test the classes. The second level of testing is called integration testing, and it tests the interactions among modules. The next level of testing is called system testing, in which the entire program is tested. Finally, a special type of testing called acceptance testing shows whether the system as a whole complies with its requirements.

Unit testing is something that you have probably done before. It is closely related to some of the ideas talked about in the previous debugging section. A function is tested to make sure that it conforms to its requirements. Often with small programs, testing does not go beyond this level.

Integration testing checks many parts of a solution together

One way to perform integration tests is to make sure that the various objects within a program correctly implement the interactions in your design. Integration testing can be challenging, because there are many ways in which the objects in a program can interact. It is difficult to make sure they do what they are designed to do and nothing more.

System testing checks the integration of the solution with other systems

System testing entails running the program in the environment in which it was designed to work. Here the program is tested to make sure that it interacts with external systems correctly. The external systems might be other programs—such as a government tax collection system—or hardware devices.

### B.7.2 Kinds of Testing

Two kinds of testing can be applied to a system:

- Open-box testing. With open-box, white-box, or glass-box testing, you design tests knowing how the modules work. You carefully choose a method's actual arguments in a way that exercises all lines of code in the method. For example, you must make sure that all branches of if and switch statements are executed.

- Closed-box testing. With closed-box, black-box, or functional testing, you know the name of the method being tested, as well as its argument list, its return type, and its operation contract. Using only this information, you develop tests across a range of valid input, and then check the output against hand-calculated results. Choosing some actual arguments outside of their valid range tests how the module handles incorrect input.

### B.7.3 Developing Test Data

The test data that you use must test a wide range of conditions. It should include valid, typical input and values at the extreme limits of valid data—called boundary values—as well as values that
