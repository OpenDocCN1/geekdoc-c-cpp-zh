
- When invoking a function, the actual arguments must correspond to the parameters in number, order, and type.

- A function makes local copies of the values of any arguments that are passed by value. Thus, the arguments remain unchanged by the function. Such arguments are, therefore, input arguments. A function does not copy arguments that are passed by reference. Rather, it references the actual argument locations whenever the parameters appear in the function definition. In this way, a function can change the values of the arguments, thus implementing output arguments. However, a function does not copy and cannot change a constant reference argument. If copying an input argument would be expensive, make it a constant reference argument instead of a value argument.

- The general form of the if statement is

  ```
  if (expression)
      statement1
  else
      statement2
  ```

  If expression is true, statement1 executes; otherwise statement2 executes.

- The general form of the switch statement is

  ```
  switch (expression)
  {
      case constant1:
          statement1;
          break;
      ...
      case constantn:
          statementn;
          break;
      default:
          statement
  }
  ```

  The appropriate statement executes according to the value of expression. Typically, break (or sometimes return) follows the statement or statements after each case. Omitting break causes execution to continue to the statement(s) after the next case.

- The general form of the while statement is

  ```
  while (expression)
      statement
  ```

  As long as expression is true, statement executes. Thus, it is possible that statement never executes.

- The general form of the for statement is

  ```
  for (initialize; test; update)
      statement
  ```

  where initialize, test, and update are expressions. Typically, initialize is an assignment expression that occurs only once. Then if test, which is usually a logical expression, is true, statement executes. The expression update executes next, usually incrementing or decrementing a counter. This sequence of events repeats, beginning with the evaluation of test, until test is false.

- 15. The general form of the do statement is

  ```
  do
  statement
  while (expression);
  ```

  Here, statement executes until the value of expression is false. Note that statement always executes at least once. Also note the required semicolon.

- 16. An array is a container of items that have the same data type. You can refer to these items by using an index that begins with zero. Arrays are always passed to functions by reference.

- 17. A string is a sequence of characters. You can manipulate the entire string, a substring, or the individual characters.

- 18. You must be careful that an array index does not exceed the size of the array. C++ does not check the range of array indices. Similar comments apply to strings.

- 19. An object encapsulates both data and operations on that data. In C++, objects are instances of a class, which is a programmer-defined data type.

- 20. A C++ class contains at least one constructor, which is an initialization method, and a destructor, which is a cleanup method that destroys an object when its lifetime ends.

- 21. If you do not define a constructor for a class, the compiler will generate a default constructor—that is, one without arguments—for you. If you do not define a destructor, the compiler will generate one for you. Chapter 4 describes when you need to write your own destructor.

- 22. Members of a class are private unless you designate them as public. The client of the class—that is, the program that uses the class—cannot use members that are private. However, the implementations of methods can use them. You should make the data members of a class private and provide public methods to access some or all of the data members.

- 23. Because certain classes have applications in many programs, you should take steps to facilitate their use. You can define and implement a class within header and implementation files, which a program can include when it needs to use the class.

- 24. A typical C++ program uses header files that you incorporate by using the #include directive. A header file contains class definitions, function declarations, constant definitions, typedef statements, enumerations, and other #include statements. The program might also require an implementation file of function definitions that have been compiled previously and placed into a library. The operating system locates the required implementation file and combines it with the program in ways that are system dependent.

## Important Themes in Programming

- Contents
- B.1 Modularity 722
- B.2 Style 723
- B.2.1 Use of Private Data Members 723
- B.2.2 Proper Use of Reference Arguments 724
- B.2.3 Proper Use of methods 724
- B.2.4 Avoidance of Global Variables in Modules 726
- B.2.5 Error Handling 726
- B.2.6 Readability 726
- B.2.7 Documentation 728
- B.3 Modifiability 729
- B.3.1 Named Constants 730
- B.3.2 The typedef Statement 730
- B.4 Ease of Use 730
- B.5 Fail-Safe Programming 731
- B.5.1 Guarding Against Errors in Input Data 732
- B.5.2 Guarding Against Errors in Program Logic 734
- B.6 Debugging 736
- B.6.1 Debugging Functions and Methods 737
- B.6.2 Debugging Loops 737
- B.6.3 Debugging if Statements 737
- B.6.4 Using cout Statements 737
- B.6.5 Using Special Dump Functions 737
- B.7 Testing 738
- B.7.1 Levels of Testing 738
- B.7.2 Kinds of Testing 738
- B.7.3 Developing Test Data 738
- B.7.4 Testing Techniques 739
- B.7.5 Use of Drivers 740

## Prerequisites

- Appendix A Review of C++ Fundamentals
- Chapter 1 Data Abstraction: The Walls

**What** are the specific characteristics of good solutions? How can you construct good solutions? This appendix provides some answers to these very difficult questions.
The programming themes that we will discuss should be familiar to you. However, the novice programmer usually does not truly appreciate their importance. After the first course in programming, many students still simply want to “get the thing to run.” The discussion that follows should help you realize just how important these themes really are.
One of the most widespread misconceptions held by novice programmers is that a computer program is “read” only by a computer. As a consequence, they tend to consider only whether the computer is able to “understand” the program—that is, does the program compile, execute, and produce the correct output? The truth is, of course, that other people often must read and modify programs. In a typical programming environment, many individuals share a program. One person may write a program, which other people use in conjunction with other programs written by other people, and a year later, a different person may modify the program. It is therefore essential that you take great care to design a program that is easy to read and understand.
You should always keep in mind the following seven themes of programming: modularity, style, modifiability, ease of use, fail-safe programming, debugging, and testing.

**People read programs, too**

**Key programming themes**

## B.1 Modularity

As this book continually emphasizes, you should strive for modularity in all phases of the problem-solving process, beginning with the initial design of a solution. Many programming tasks become more difficult as the size and complexity of a program grows. Modularity slows the rate at which the level of difficulty grows. More specifically, modularity has a favorable impact on the following aspects of programming:

### Modularity facilitates programming

- **Constructing the program.** The primary difference between a small modular program and a large modular program is simply the number of modules each contains. Because the modules are independent, writing one large modular program is not very different from writing many small, independent programs, although the interrelationships among modules make the design much more complicated. On the other hand, working on a large nonmodular program is more like working on many interrelated programs simultaneously. Modularity also permits team programming, in which several programmers work independently on their own modules before combining them into one program.

### Modularity isolates errors

- **Debugging the program.** Debugging a large program can be a monstrous task. Imagine that you try a 10,000-line program and eventually get it to compile. Neither of these tasks would be much fun. Now imagine that you execute your program, and after a few hundred lines of output, you notice an incorrect number. You should anticipate spending the next day or so tracing through the intricacies of your program before discovering a problem such as an array index that is too large.
A great advantage of modularity is that the task of debugging a large program is reduced to one of debugging many small programs. When you begin to code a module, you should be almost certain that all other modules coded so far are correct. That is, before you consider a module finished, you should test it extensively, both separately and in context with the other modules, by calling it with actual arguments carefully chosen to induce all possible behaviors of the modules. If this testing is done thoroughly, you can feel fairly sure that any problem is a result of an error in the last module added. Modularity isolates errors.
