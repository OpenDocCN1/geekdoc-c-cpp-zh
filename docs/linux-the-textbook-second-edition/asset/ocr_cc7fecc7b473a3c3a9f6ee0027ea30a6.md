# 14.5.3.4 Compiling and Executing C++ and Java Programs

You can use the g++ compiler to compile C++ programs. However, it is not preinstalled in Linux Mint 18. You can ask your system administrator to install it for you. If you have superuser privileges, you can install it yourself as described in Appendix A.

The file containing C++ source must have one of the following extensions: .C, .CPP, .cpp, .C++, or .cc. In the following session, we show a small C++ program, its compilation, and execution.

```
$ more Hello.cpp
// My first C++ program on Mint 18 Linux
#include <iostream>

int main()
{
    std::cout << "Hello, World!\n";
    return 0;
}
$ g++ Hello.cpp -o Hello
$ Hello
Hello, World!
$
```

Java source code is compiled (translated) into Java bytecode and is interpreted by the Java Virtual Machine (JVM), also known as the Java Interpreter. The Java compiler on our Linux system is called javac, and the JVM is java. Thus, to run a Java program in a file, say Hello.java, we use the javac compiler to compile it. It produces the Java bytecode and stores it in the Hello.class file, which is interpreted with the java command, as shown in the following session.

```
$ more Hello.java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
        System.exit(0);
    }
}
$ javac Hello.java
$ java Hello
Hello, world!
$
```

In the following in-chapter exercises, you will use the gcc, g++, and javac compiler commands to compile simple C, C++, and Java programs on your Linux system and run them.

# Exercise 14.2

Replicate all of the sessions discussed in Sections 14.5.3.1–14.5.3.4 on your system to verify that they work as expected.

# Exercise 14.3

Create simple C, C++, and Java programs on your Linux system. Compile and run them to appreciate the basic working of the two compilers (gcc and javac) and the Java Virtual Machine, java.

# 14.5.3.5 Running Perl, Python, and Ruby Scripts

You can run Perl, Python, and Ruby scripts on Linux by using their interpreters. The interpreters for Perl, Python, and Ruby are /usr/bin/perl, /usr/bin/python, and /usr/bin/python, which may be invoked