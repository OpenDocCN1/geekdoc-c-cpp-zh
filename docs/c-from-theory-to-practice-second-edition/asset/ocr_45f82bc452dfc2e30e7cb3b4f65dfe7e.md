# 19

# Introduction to Java

This chapter introduces you to Java and discusses some of its most important features. If you skipped the C++ introduction it'd be better to go back and read it, in order to get familiar with the basic object-oriented concepts. The implementation examples we are using are quite similar, in order to become easier for you to see how the same features are supported in both languages and compare the code.

James Gosling and his colleagues, Mike Sheridan and Patrick Naughton, initiated the Java language project in Sun Microsystems labs in 1991, in the framework of Stealth Project, which was then renamed to Green Project. The aim of Green Project was the creation of a revolutionary object-oriented programming language. The language was initially called Greentalk and it was then renamed to Oak, because of an oak tree that stood outside Gosling's office, while in 1994, it was finally renamed to Java, inspired by Java coffee and the love of the development team for the coffee.

Recall that in C/C++, the source code is translated into machine language, which depends on the computer architecture. For example, a C executable program compiled in Unix environment cannot run as is in Windows environment, in order to generate the new executable. The source code has to be recompiled.

On the other hand, Java is a portable and cross-platform programming language, meaning that a Java program may run on any system without having to recompile the program. The only requirement set for the system is to support the Java Virtual Machine (JVM). The source code is compiled into an “intermediate” specialized format called bytecode, which is the machine language of a virtual architecture and specifically that of JVM. The JVM is responsible to translate real time, that is, during the execution of the Java program, the bytecode into the system's machine language.

# Classes and Objects

The extension of Java source files is .java, while, after successful compilation, class files (one per each defined class) with .class extension are produced. Let's see our first Java program:

```
```java
class MainClass {
    // This is my first Java program
    public static void main(String[] args) {
        System.out.println("D. Bowie: Space Oddity");
    }
}
```
```

Listen to D. Bowie and let's start our short tour of the Java planet. Suppose that our program resides in the MainClass.java file. Notice that the name of the file has to be the