
Array name with two different indices in them. For example, we can pull values out of tda2 in this way.

```
scala tda3(3)(4)
res0: Int = 12
```

The D-2 Array tda3 was to be something like a multiplication table. This particular expression pulled the element at position 3,4 which is 12. To understand why you use this syntax, think of the types shown here.

```scala
scala tda3(3)
res33: Array[Int] = Array(0, 3, 6, 9, 12, 15, 18, 21, 24)
```

```scala
scala tda3(3)(4)
res34: Int = 12
```

The original value is an Array [Array[Int]]. When you index into an Array you get back an instance of the type it is. In that case, means that tda(3) has the type Array[Int]. Indexing that gets down to a single Int.

The advantages and restrictions of the List and Array types were introduced in chapter 6 apply to higher dimensional cases as well. Once you make an Array, the values can be changed, but the length cannot. Similarly, you can make new Lists by efficiently adding to the head of old ones, but you cannot mutate values in a List even if it has a higher dimension.

## 7.11 Classifying Bugs

By this you have learned that writing your code does not mean that it is correct and that it works. Errors in programs are generally referred to as bugs. The term has a long history in the engineering field. It came into the field of computer science early because one of the first was a moth. The earliest computers were huge. They took up the size of gymiums. An malfunction in one turned out to be a moth that had flown in and was causing a short circuit.

When the "bug" has stuck around, the implications of this term no longer fit. The term and its history imply it is something beyond the control of the programmer that just it into the code and now the programmer needs to search for it. In reality, virtually all modern bugs are mistakes on the programmer. They are things that the programmer put into the code and now the programmer needs to correct.

Not all bugs are the same. There are three fundamentally different types of errors.

- 1. SYNTAX ERROR – Error in the structure of the code that is found by the compiler. If you have a syntax error it means your program is not valid for the language you are writing in, for our purposes that is Scala.
- 2. RUNTIME ERROR – Error that causes the program to crash while running.
- 3. LOGIC ERROR – Error that does not crash the code, but it causes it to produce the wrong answer.

Each of these deserves some discussion. We will also talk about how they compare to another and the way in which they impact programs.

When you are first learning to program, the errors that you likely run into the most are syntax errors. These can be simple typos or misspellings. They can also be complex like type mismatches or calling functions or methods with the wrong number of arguments. The common element that makes a syntax error is that it is discovered by the compiler when it is trying to translate the human written code into a format that is more computer friendly. Different programming languages do different amounts of checking for errors at compile time. This is often called STATIC CHECKING because it can be done without actually running the program.

Scala does a significant amount of static checking for errors.¹¹⁰ The way we have running our programs in the REPL or with scripts, the compile stage is not clearly separated from the running of the program. The Scala system is running a compiler in the background and executing the results of the compile. The syntax errors display a message like the following:

```
timing.scala:5: error: not found: value This
This line will not compile
- one error found
```

They tell you the name of the file with a line number. Then they describe the error and show the line and where the line error occurred.

The second type of bug is a runtime error. This type of error occurs when everything is syntactically correct and the program compiles and runs. During during the run the error causes the program to crash. In Scala, a runtime error will produce a message that looks similar to the following:

```
java.lang.ArrayIndexOutOfBoundsException: -1
at Main$anon1.<init>(timing.scala:5)
at Main$main(timing.scala:1)
at Main$main(timing.scala)
```

This tells you what you wrote and then prints something called the code failed on line 5. The stack trace includes line numbers. The stack trace shows the line of code that was currently executing at the top, followed by the line that called that function, and so on. Sometimes the line is not in your code, but something you passed into a library call. You can look down the stack trace to find the first line that is in your code for guidance on what is causing the problem.

There are many different reasons why runtime errors happen, and it might be dependent on user input. So a runtime error might not be found running the program or twice.

¹⁰ The significant static checking of types was a major influence in the selection of Scala for this textbook. Other introductory languages, like Python, do significantly less static checking of programs.

To reduce the number of runtime errors in a program is to run it with multiple test inputs. This will be discussed in more detail in section 8.4. In a general sense, it is impossible to prove that code has no runtime errors.

The last type of error is a logic error. An error is a logic error if the code compiles and runs to normal termination, but provides an incorrect output or behaves incorrectly. These errors can occur in all types of forms, and there is no message that tells you there is a problem. You know there by checking the output or behavior of the program to see if it matches. Unlike runtime errors, logic errors might not occur for all inputs. There might be only specific inputs that trigger the error.

If you have a choice, you want to fix errors earlier on this list. As a novice programmer you probably got tired of syntax errors and found them frustrating, the reality is that syntax errors are the best type of error. This is because syntax errors give you the most information on how to fix them and are detected by the compiler do not depend on inputs. Your second choice would be a runtime error for some of the same reasons, it provides you with some information related to what is wrong and, as a result, helps you fix the problem. By contrast, logic errors provide no information on how to fix or where they are. This makes logic errors very challenging to fix, especially in large programs.

Different languages do more or less to help you with error detection. One of the significant advantages of Scala is that it is designed to maximize the number of syntax errors and reduce the number of runtime and logic errors. Part of this is due to the type checking of Scala. The language does significant type checking to make sure that all the values you use are of a type that is appropriate for the usage.

Many of the order functions and methods in Scala also help to prevent common errors that face in other languages. This is also true of rules such as the requirement to initialize at declaration and the general preference of val declarations var declarations. To understand this, simply consider the following line of code:

```scala
val dbl = nums.filter(_>0.5).map(*2)
```

This line of code will give us a new collection of numbers that are twice the magnitude of the elements but for the elements that were originally greater than 0.5. There are not too many ways to mess up this line without having it a syntax error. It is possible to get a logic error if you mistake the greater than or the multiplication, but that is nothing no programming language can really fix. The programmer has to correctly communicate the logic error, but this line does not have all that other than logic can catch. Despite this, it is easy to read for anyone who has experience with map and filter.

To understand the real value of this line of code, you have to consider the alternative, which is what you would have to write in most other programming languages that do not provide map and filter if you simply choose not to use them. We would write equivalent code that is simple The Scala code works equally well for any sequence, but we will ignore that advantage for now.

```
var cnt = 0
for (i < 0 nums.length) {
  if (nums(i) > 0.5) cnt += 1
}
val dbl = Array.fill(cnt)(0.0)
cnt = 0
for (i < 0 nums.length) {
  if (nums(i) > 0.5) {
    dbl(cnt) = nums(i)*2
```
