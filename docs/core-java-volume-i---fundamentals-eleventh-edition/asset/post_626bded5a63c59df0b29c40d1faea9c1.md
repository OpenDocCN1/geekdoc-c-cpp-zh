
The `$1` in the output indicates that the result is available in further calculations. For example, if you type

```
5 * $1 - 3
```

the response is

```
$2 ==> 42
```

If you need a variable many times, you can give it a more memorable name. However, you have to follow the Java syntax and specify both the type and the name. (We will cover the syntax in Chapter 3.) For example,

```
jshell> int answer = 6 * 7
answer ==> 42
```

Another useful feature is tab completion. Type

```
Math.
```

followed by the Tab key. You get a list of all methods that you can invoke with the Math class:

```text
jshell> Math.
E                  IEEEremainder(      PI             abs(
acos(              addExact(          asin(          atan(
atan2(             cbrt(              ceil(          class
copySign(           cos(               cosh(          decrementExact(
exp(               expm1(              floor(         floorDiv(
floorMod(           fma(                getExponent(   hypot(
incrementExact(     log(                log10(         max(
min(               multiplyExact(     multiplyFull(  multiplyHigh(
negateExact(       nextAfter(         nextDown(      nextUp(
pow(               random(            rint(          round(
scalb(             signum(            sin(           sinh(
sqrt(              subtractExact(     tan(           tanh(
toDegrees(         toIntExact(        toRadians(     ulp(
```

Now type `l` and hit the Tab key again. The method name is completed to log, and you get a shorter list:

```text
jshell> Math.log
log(     log10(   log1p(
```

Now you can fill in the rest by hand:

```
jshell> Math.log10(0.001)
$3 ==> -3.0
```

To repeat a command, hit the ↑ key until you see the line that you want to reissue or edit. You can move the cursor in the line with the ← and → keys, and add or delete characters. Hit Enter when you are done. For example, hit ↑ and replace 0.001 with 1000, then hit Enter:

```
jshell> Math.log10(1000)
$4 ==> 3.0
```

JShell makes it easy and fun to learn about the Java language and library without having to launch a heavy-duty development environment and without fussing with public static void main.

In this chapter, you learned about the mechanics of compiling and running Java programs. You are now ready to move on to Chapter 3 where you will start learning the Java language.

*This page intentionally left blank*

## CHAPTER 3

## Fundamental Programming Structures in Java

### In this chapter

- 3.1 A Simple Java Program, page 38
- 3.2 Comments, page 41
- 3.3 Data Types, page 42
- 3.4 Variables and Constants, page 48
- 3.5 Operators, page 52
- 3.6 Strings, page 62
- 3.7 Input and Output, page 75
- 3.8 Control Flow, page 86
- 3.9 Big Numbers, page 105
- 3.10 Arrays, page 108

At this point, we are assuming that you successfully installed the JDK and were able to run the sample programs that we showed you in Chapter 2.

It’s time to start programming. This chapter shows you how the basic programming concepts such as data types, branches, and loops are implemented in Java.

### 3.1 A Simple Java Program

Let’s look more closely at one of the simplest Java programs you can have—one that merely prints a message to console:

```java
public class FirstSample
{
    public static void main(String[] args)
    {
        System.out.println("We will not use 'Hello, World!'");
    }
}
```

It is worth spending all the time you need to become comfortable with the framework of this sample; the pieces will recur in all applications. First and foremost, *Java is case sensitive*. If you made any mistakes in capitalization (such as typing Main instead of main), the program will not run.

Now let’s look at this source code line by line. The keyword `public` is called an *access modifier*; these modifiers control the level of access other parts of a program have to this code. We’ll have more to say about access modifiers in Chapter 5. The keyword `class` reminds you that everything in a Java program lives inside a class. Although we will spend a lot more time on classes in the next chapter, for now think of a class as a container for the program logic that defines the behavior of an application. As mentioned in Chapter 1, classes are the building blocks with which all Java applications and applets are built. *Everything* in a Java program must be inside a class.

Following the keyword `class` is the name of the class. The rules for class names in Java are quite generous. Names must begin with a letter, and after that, they can have any combination of letters and digits. The length is essentially unlimited. You cannot use a Java reserved word (such as `public` or `class`) for a class name. (See the appendix for a list of reserved words.)

The standard naming convention (which we follow in the name `FirstSample`) is that class names are nouns that start with an uppercase letter. If a name consists of multiple words, use an initial uppercase letter in each of the words. (This use of uppercase letters in the middle of a word is sometimes called "camel case" or, self-referentially, "CamelCase".)

You need to make the file name for the source code the same as the name of the public class, with the extension `.java` appended. Thus, you must store this code in a file called `FirstSample.java`. (Again, case is important—don't use `firstsample.java`.)

If you have named the file correctly and not made any typos in the source code, then when you compile this source code, you end up with a file containing the bytecodes for this class. The Java compiler automatically names the bytecode file `FirstSample.class` and stores it in the same directory as the source file. Finally, launch the program by issuing the following command:

```text
java FirstSample
```

(Remember to leave off the `.class` extension.) When the program executes, it simply displays the string We will not use 'Hello, World!' on the console.

When you use

```text
java ClassName
```

to run a compiled program, the Java virtual machine always starts execution with the code in the `main` method in the class you indicate. (The term “method” is Java-speak for a function.) Thus, you *must* have a `main` method in the source of your class for your code to execute. You can, of course, add your own methods to a class and call them from the `main` method. (We cover writing your own methods in the next chapter.)

> **NOTE:** According to the Java Language Specification, the `main` method must be declared `public`. (The Java Language Specification is the official document that describes the Java language. You can view or download it from http://docs.oracle.com/javase/specs).
>
> However, several versions of the Java launcher were willing to execute Java programs even when the `main` method was not `public`. A programmer filed a bug report. To see it, visit http://bugs.java.com/bugdatabase/index.jsp and enter the Bug ID 4252539. In 1999, that bug was marked as “closed, will not be fixed.” A Sun engineer added an explanation that the Java Virtual Machine Specification (at http://docs.oracle.com/javase/specs/jvms/se8/html) does not mandate that `main` is `public` and that “fixing it will cause potential troubles.” Fortunately, sanity finally prevailed. The Java launcher in Java 1.4 and beyond enforces that the `main` method is `public`.
>
> There are a couple of interesting aspects about this story. On the one hand, it is frustrating to have quality assurance engineers, who are often overworked and not always experts in the fine points of Java, make questionable decisions about bug reports. On the other hand, it is remarkable that Sun made the bug reports and their resolutions available for anyone to scrutinize, long before Java was open source. At one point, Sun even let programmers vote for their most despised bugs and used the vote counts to decide which of them would get fixed in the next JDK release.

Notice the braces `{}` in the source code. In Java, as in C/C++, braces delineate the parts (usually called *blocks*) in your program. In Java, the code for any method must be started by an opening brace `{` and ended by a closing brace `}`.

Brace styles have inspired an inordinate amount of useless controversy. We follow a style that lines up matching braces. As whitespace is irrelevant to the Java compiler, you can use whatever brace style you like. We will have more to say about the use of braces when we talk about the various kinds of loops.

For now, don’t worry about the keywords `static` `void`—just think of them as part of what you need to get a Java program to compile. By the end of Chapter 4, you will understand this incantation completely. The point to remember for now is that every Java application must have a main method that is declared in the following way:

```java
public class ClassName
{
    public static void main(String[] args)
    {
        *program statements*
    }
}
```

![](img/127bccebb2cfadea3f02579edaad63c3_66_0.png)

> **C++ NOTE:** As a C++ programmer, you know what a class is. Java classes are similar to C++ classes, but there are a few differences that can trap you. For example, in Java all functions are methods of some class. (The standard terminology refers to them as methods, not member functions.) Thus, in Java you must have a shell class for the main method. You may also be familiar with the idea of static *member functions* in C++. These are member functions defined inside a class that do not operate on objects. The main method in Java is always static. Finally, as in C/C++, the void keyword indicates that this method does not return a value. Unlike C/C++, the main method does not return an “exit code” to the operating system. If the main method exits normally, the Java program has the exit code 0, indicating successful completion. To terminate the program with a different exit code, use the `System.exit` method.
