# Declaring a Method

Line 6

```
```java
// main method begins execution of Java application
```
```

is an end-of-line comment indicating the purpose of lines 7–10 of the program. Line 7

```
```java
public static void main( String[] args )
```
```

is the starting point of every Java application. The parentheses after the identifier **main** indicate that it’s a program building block called a **method**. Java class declarations normally contain one or more methods. For a Java application, one of the methods must be called **main** and must be defined as shown in line 7; otherwise, the Java Virtual Machine (JVM) will not execute the application. Methods perform tasks and can return information when they complete their tasks. Keyword **void** indicates that this method will *not* return any information. Later, we’ll see how a method can return information. For now, simply mimic **main**’s first line in your Java applications. In line 7, the `String[] args` in parentheses is a required part of the method **main**’s declaration—we discuss this in Chapter 7.

The left brace in line 8 begins the body of the **method declaration**. A corresponding right brace must end it (line 10). Line 9 in the method body is indented between the braces.

# Performing Output with `System.out.println`

Line 9

```
```java
System.out.println( "Welcome to Java Programming!" );
```
```

instructs the computer to perform an action—namely, to print the **string** of characters contained between the double quotation marks (but not the quotation marks themselves). A string is sometimes called a **character string** or a **string literal**. White-space characters in strings are *not* ignored by the compiler. Strings cannot span multiple lines of code, but as you’ll see later, this does not restrict you from using long strings in your code.

The **System.out** object is known as the **standard output object**. It allows a Java application to display information in the command window from which it executes. In recent versions of Microsoft Windows, the command window is the **Command Prompt**. In UNIX/Linux/Mac OS X, the command window is called a **terminal window** or a **shell**. Many programmers call it simply the **command line**.

Method **System.out.println** displays (or prints) a line of text in the command window. The string in the parentheses in line 9 is the argument to the method. When **System.out.println** completes its task, it positions the output cursor (the location where the next character will be displayed) at the beginning of the next line in the command

> **Good Programming Practice 2.4**
> 
> Many IDEs insert indentation for you in all the right places. The Tab key may also be used to indent code, but tab stops vary among text editors. Most IDEs allow you to configure tabs such that a specified number of spaces is inserted each time you press the Tab key.

> **Good Programming Practice 2.5**
> 
> Indent the entire body of each method declaration one “level” between the braces that define the body of the method. This makes the structure of the method stand out and makes the method declaration easier to read.