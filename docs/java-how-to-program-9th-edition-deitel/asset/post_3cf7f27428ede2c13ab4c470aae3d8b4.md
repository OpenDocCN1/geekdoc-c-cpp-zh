
// Fig. 8.14: StaticImportTest.java
// Static import of Math class methods.
import static java.lang.Math.*;

public class StaticImportTest
{
    public static void main( String[] args )
    {
        System.out.printf( "sqrt( 900.0 ) = %.1f\n", sqrt( 900.0 ) );
        System.out.printf( "ceil( -9.8 ) = %.1f\n", ceil( -9.8 ) );
        System.out.printf( "E = %f\n", E );
        System.out.printf( "PI = %f\n", PI );
    } // end main
} // end class StaticImportTest

```
sqrt( 900.0 ) = 30.0
ceil( -9.8 ) = -9.0
log( E ) = 1.0
cos( 0.0 ) = 1.0
```

Fig. 8.14 | Static import of Math class methods.

## 8.13 final Instance Variables

The principle of least privilege is fundamental to good software engineering. In the context of an application, it states that code should be granted only the amount of privilege and access that it needs to accomplish its designated task, but no more. This makes your programs more robust by preventing code from accidentally (or maliciously) modifying variable values and calling methods that should not be accessible.

Let’s see how this principle applies to instance variables. Some of them need to be modifiable and some do not. You can use the keyword final to specify that a variable is not modifiable (i.e., it’s a constant) and that any attempt to modify it is an error. For example,

```
private final int INCREMENT;
```

declares a final (constant) instance variable INCREMENT of type int. Such variables can be initialized when they’re declared. If they are not, they must be initialized in every constructor of the class. Initializing constants in constructors enables each object of the class to have a different value for the constant. If a final variable is not initialized in its declaration or in every constructor, a compilation error occurs.

> Software Engineering Observation 8.9
> Declaring an instance variable as final helps enforce the principle of least privilege. If an instance variable should not be modified, declare it to be final to prevent modification.

> Common Programming Error 8.10
> Attempting to modify a final instance variable after it’s initialized is a compilation error.

## Error-Prevention Tip 8.4

Attempts to modify a final instance variable are caught at compilation time rather than causing execution-time errors. It’s always preferable to get bugs out at compilation time, if possible, rather than allow them to slip through to execution time (where experience has found that repair is often many times more expensive).

## Software Engineering Observation 8.10

A final field should also be declared static if it’s initialized in its declaration to a value that’s the same for all objects of the class. After this initialization, its value can never change. Therefore, we don’t need a separate copy of the field for every object of the class. Making the field static enables all objects of the class to share the final field.

## 8.14 Time Class Case Study: Creating Packages

We’ve seen in almost every example in the text that classes from preexisting libraries, such as the Java API, can be imported into a Java program. Each class in the Java API belongs to a package that contains a group of related classes. These packages are defined once, but can be imported into many programs. As applications become more complex, packages help you manage the complexity of application components. Packages also facilitate software reuse by enabling programs to import classes from other packages (as we’ve done in most examples), rather than copying the classes into each program that uses them. Another benefit of packages is that they provide a convention for unique class names, which helps prevent class-name conflicts (discussed later in this section). This section introduces how to create your own packages.

## Steps for Declaring a Reusable Class

Before a class can be imported into multiple applications, it must be placed in a package to make it reusable. Figure 8.15 shows how to specify the package in which a class should be placed. Figure 8.16 shows how to import our packaged class so that it can be used in an application. The steps for creating a reusable class are:

- 1. Declare a public class. If the class is not public, it can be used only by other classes in the same package.
- 2. Choose a unique package name and add a package declaration to the source-code file for the reusable class declaration. In each Java source-code file there can be only one package declaration, and it must precede all other declarations and statements. Comments are not statements, so comments can be placed before a package statement in a file. [Note: If no package statement is provided, the class is placed in the so-called default package and is accessible only to other classes in the default package that are located in the same directory. All prior programs in this book having two or more classes have used this default package.]
- 3. Compile the class so that it’s placed in the appropriate package directory.
- 4. Import the reusable class into a program and use the class.

We’ll now discuss each of these steps in detail.

## Steps 1 and 2: Creating a public Class and Adding the package Statement

For Step 1, we modify the public class Time1 declared in Fig. 8.1. The new version is shown in Fig. 8.15. No modifications have been made to the implementation of the class, so we’ll not discuss its implementation details again here.

For Step 2, we add a package declaration (line 3) that declares a package named com.deitel.jhtp.ch08. Placing a package declaration at the beginning of a Java source file indicates that the class declared in the file is part of the specified package. Only package declarations, import declarations and comments can appear outside the braces of a class declaration. A Java source-code file must have the following order:

```
// Fig. 8.15: Time1.java
// Time1 class declaration maintains the time in 24-hour format.
package com.deitel.jhtp.ch08;

public class Time1
{
    private int hour; // 0 - 23
    private int minute; // 0 - 59
    private int second; // 0 - 59

    // set a new time value using universal time; throw an
    // exception if the hour, minute or second is invalid
    public void setTime( int h, int m, int s )
    {
        // validate hour, minute and second
        if ( ( h >= 0 && h < 24 ) && ( m >= 0 && m < 60 ) &&
             ( s >= 0 && s < 60 ) )
        {
            hour = h;
            minute = m;
            second = s;
        } // end if
        else
            throw new IllegalArgumentException(
                "hour, minute and/or second was out of range");
    } // end method setTime

    // convert to String in universal-time format (HH:MM:SS)
    public String toUniversalString()
    {
        return String.format( "%02d:%02d:%02d", hour, minute, second );
    } // end method toUniversalString

    // convert to String in standard-time format (H:MM:SS AM or PM)
    public String toString()
    {
        return String.format( "%d:%02d:%02d %s",
            ( ( hour == 0 || hour == 12 ) ? 12 : hour % 12 ),
            minute, second, ( hour < 12 ? "AM" : "PM" ) );
    } // end method toString
} // end class Time1
```

Fig. 8.15 | Packaging class Time1 for reuse.

- 1. a package declaration (if any),
- 2. import declarations (if any), then
- 3. class declarations.

Only one of the class declarations in a particular file can be public. Other classes in the file are placed in the package and can be used only by the other classes in the package. Non-public classes are in a package to support the reusable classes in the package.

To provide unique package names, start each one with your Internet domain name in reverse order. For example, our domain name is deitel.com, so our package names begin with com.deitel. For the domain name yourcollege.edu, the package name should begin with edu.yourcollege. After the domain name is reversed, you can choose any other names you want for your package. If you’re part of a company with many divisions or a university with many schools, you may want to use the name of your division or school as the next name in the package. We chose to use jhtp as the next name in our package name to indicate that this class is from Java How to Program. The last name in our package name specifies that this package is for Chapter 8 (ch08).

## Step 3: Compiling the Packaged Class

Step 3 is to compile the class so that it’s stored in the appropriate package. When a Java file containing a package declaration is compiled, the resulting class file is placed in the directory specified by the declaration. The package declaration in Fig. 8.15 indicates that class Time1 should be placed in the directory

```
com
    deitel
        jhtp
            ch08
```

The names in the package declaration specify the exact location of the package’s classes.

When compiling a class in a package, the javac command-line option -d causes the javac compiler to create appropriate directories based on the class’s package declaration. The option also specifies where the directories should be stored. For example, in a command window, we used the compilation command

```
javac -d . Time1.java
```

to specify that the first directory in our package name should be placed in the current directory. The period (.) after -d in the preceding command represents the current directory on the Windows, UNIX, Linux and Mac OS X operating systems (and several others as well). After execution of the compilation command, the current directory contains a directory called com, com contains a directory called deitel, deitel contains a directory called jhtp and jhtp contains a directory called ch08. In the ch08 directory, you can find the file Time1.class. [Note: If you do not use the -d option, then you must copy or move the class file to the appropriate package directory after compiling it.]

The package name is part of the fully qualified class name, so the name of class Time1 is actually com.deitel.jhtp.ch08.Time1. You can use this fully qualified name in your programs, or you can import the class and use its simple name (the class name by itself—Time1) in the program. If another package also contains a Time1 class, the fully qualified class names can be used to distinguish between the classes in the program and prevent a name conflict (also called a name collision).
