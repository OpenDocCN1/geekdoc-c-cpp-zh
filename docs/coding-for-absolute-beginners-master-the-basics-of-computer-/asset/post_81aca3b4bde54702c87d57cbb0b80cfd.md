
## For Loop

For Loop is used to perform iteration in a part of the program. If the number of iterations is fixed, you are advised to use For Loop in your program.

## While Loop

While Loop has the characteristics to repeat a single or group of statements to test whether the given condition is true or not. It is used when the number of iterations is not fixed.

## Do While Loop

The Do While Loop is used to iterate a part of a program several times. If the number of iterations is not fixed, you are required to execute the program at least once.

There are specific loop control statements that are required to change the execution into a normal sequence. The two control statements used in Java programming language include:

- Break statement: Terminates the switch or loop to start the next loop.
- Continue statement: Allows the loop to retest its condition and skip the rest of the body.

## Decision Making

The decision-making structure features one or more conditions that need to be tested under a given scenario. If the condition is true, the next statement can be executed whereas the program would terminate if the given condition is false. The diagram below correctly shows how the decision-making process actually works:

## Characters, Strings, Arrays, and Regular Expressions

Java programming language makes use of Character wrapper class and offers multiple static methods for manipulating characters. To create a character object, you need to follow the syntax as follows:

`Character ch = new Character('a');`

The compiler will automatically create a Character object and if you pass any primitive char into the method, the compiler will convert the Char into Character by using various approaches from the language.

As we have discussed the importance and functionality of strings before, Java platform also provides the support from string class. Programmers can manipulate strings in multiple ways. The sample code for creating a string in the Java language is as follows:

```java
public class NewString {
    public static void main(String args[]) {
        char[] StudentArray = { 'S', 'T', 'U', 'D', 'E', 'N', 'T'};
        String StudentString = new String(StudentArray);
        System.out.println(StudentString );
    }
}
```

The output for this program is: STUDENT.

Moreover, we can also concatenate strings by using a simple concatenation approach in Java programming language as follows:

`String1.concat(string2);`

To create a string object in Java, programmers can choose either a literal or keyword approach.

### Arrays

Arrays are a vital part of every programming language as they allow programmers to handle and store data into variables. As they are used to store a large collection of data, you can also consider an array as a collection of variables of the same category. To declare an array, you can follow the simple syntax as briefed below:

`datatype[] arrayRefVar;`

Creating an array in Java is simple for which you can use the following syntax:

`arrayRefVar = new datatype[arraySize];`

This statement will create an array of the given size and assign the reference of this array to the given variable as well. Usually, the arrays are processed by using for loop or foreach loop because the elements inside the array are of the same type and size.

Static methods for sorting, searching, comparing, and filling array elements:

- `public static int binarySearch(Object[] a, Object key)`
- `public static void fill(int[] a, int val)`
- `public static boolean equals(long[] a, long[] a2)`
- `public static void sort(Object[] a)`

### Regular Expressions

Regular expressions is an API that is used to define string patterns and is also used for searching, editing, and manipulating text. Java has a predefined java.util.regex package that consists of a Pattern class, Matcher Class, and PatternSyntaxException object. The Pattern class requires the developers to start with the compile() methods and return a pattern object as it provides no public constructors.

For the Matcher class, the matcher object finds and compares the operations against an input string in order to obtain a Matcher object through the Matcher() method. The PatternSyntaxException is used to indicate an error or mistake in the regular expression pattern.

## Files and I/O

Java programming language features a built-in package that is responsible for data input and output operations. The stream is known as java.io and supports multiple operations and functionality to handle data. There are two general types of streams in Java which are known as Input Stream and Output Stream.

Input Stream is used to read data whereas the Output stream is used for writing data in a file.

Java language features various I/O data handling streams that include the following:

- Byte Streams
- Character Streams
- Standard Streams
- File Input Stream
- File Output Stream

## Object Oriented Java

Object Oriented Programming is an approach that includes the use of classes and objects. By using multiple concepts such as inheritance, polymorphism, Encapsulation and Abstraction, programmers can develop Java applications and programs.

### Inheritance

Inheritance is a feature in Java programming language that allows it to inherit the features and properties of another class. This can be done between the subclass and superclass. The class whose features are inherited is called the superclass whereas the class that inherits the properties of another class is called as the subclass.

To use Inheritance in Java programming language, you can follow the syntax as mentioned below:

```java
class derived-class extends base-class
{
        //methods
}
```

### Polymorphism

The technique of doing a single task in multiple ways is known as Polymorphism. In Java programming, we can use method overriding and method overloading techniques to achieve polymorphism. It is essential to know that an object can also be accessed through a reference variable and once it has been reassigned to other objects, the type of reference variable can be used to determine the method that is to be used to access the object.

For example:

```java
public interface School {}
public class Student {}
public class John extends Student implements School {}
```

In the above case, John is known to be polymorphic because it has multiple inheritance and we can apply the reference variable for the same object as well.

### Abstraction

An Abstract Class is one which includes an abstract keyword in its declaration and it may or may not contain abstract methods. In a case where a class has an abstract method, it cannot be instantiated and the programmer will have to inherit it from another class to implement the abstract method.

### Encapsulation

Encapsulation in Java programming is the process of wrapping data and methods together. Generally, the variable of one class will be hidden from another class and it can only be accessed through the methods that are being used in their current class. The advantages of encapsulation are that a class could be made read only or write only and it can also have total control over the data stored.

### Recursion

Recursion is a technique referred to a method which calls itself within the program. The recurse() method is called from the main method and can also be called from the same recurse() method as well. This process continues until the given condition is met and if the case is not satisfied, infinite recursion occurs.

Here is a simple implementation of recursion in Java:

```java
class Sample {
    static void printFun(int test)
    {
        if (test < 1)
            return;

        else {
            System.out.printf("%d ", test);

            // Statement 2
            printFun(test - 1);

            System.out.printf("%d ", test);
            return;
        }
    }
}
```

```java
}

public static void main(String[] args)
{
    int test = 3;
    printFun(test);
}
}
```

### Advantages of recursion

There are several complex programs in which writing recursive code can deliver several benefits. As it provides a simple and clean way to write code, developers can perform operations of different kinds without any hassle.

## Abstract Class and Abstract Methods

### Abstract Class

In Java programming, an Abstract class is known as a class which cannot be instantiated and is declared by using the `abstract` keyword.

Here is the syntax for declaring an abstract class *Student* in Java:

```java
abstract class Student {
    //methods and attributes
}
```

Remember that we cannot create objects of an abstract class. Doing so will generate a compilation error.

### Inheritance of Abstract class

Here is a sample Java program illustrating the inheritance of an abstract class:

```java
abstract class Student {
    public void displayInfo() {
        System.out.println("I am a Student");
    }
}
class Grade extends Student {
}
class Main {
```
