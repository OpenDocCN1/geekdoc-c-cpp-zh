
If you don't provide a handler, the program terminates and prints a message to the console, giving the type of the exception. You may have already seen exception reports when you accidentally used a null reference or overstepped the bounds of an array.

There are two kinds of exceptions: *unchecked exceptions* and *checked exceptions*. With checked exceptions, the compiler checks that you, the programmer, are aware of the exception and are prepared to deal with the consequences. However, many common exceptions, such as bounds errors, or accessing a null reference, are unchecked. The compiler does not expect that you provide a handler—after all, you should spend your mental energy on avoiding these mistakes rather than coding handlers for them.

But not all errors are avoidable. If an exception can occur despite your best efforts, then most Java APIs will throw a checked exception. One example is the `Class.forName` method. There is no way for you to ensure that a class with the given name exists. In Chapter 7, you will see several strategies for exception handling. For now, we just show you the simplest strategy.

Whenever a method contains a statement that might throw a checked exception, add a `throws` clause to the method name.

```java
public static void doSomethingWithClass(String name)
   throws ReflectiveOperationException
{
   Class cl = Class.forName(name); // might throw exception
   do something with cl
}
```

Any method that calls this method also needs a `throws` declaration. This includes the `main` method. If an exception actually occurs, the `main` method terminates with a stack trace. (You will learn in Chapter 7 how to catch exceptions instead of having them terminate your programs.)

You only need to supply a `throws` clause for checked exceptions. It is easy to find out which methods throw checked exceptions—the compiler will complain whenever you call a method that threatens to throw a checked exception and you don't supply a handler.

## 5.7.3 Resources

Classes often have associated data files, such as:

- Image and sound files
- Text files with message strings and button labels

In Java, such an associated file is called a *resource*.

For example, consider a dialog box that displays a message such as the one in Figure 5.3.

![](img/127bccebb2cfadea3f02579edaad63c3_295_0.png)

**Figure 5.3** Displaying image and text resources

Of course, the book title and copyright year in the panel will change for the next edition of the book. To make it easy to track this change, we will put the text inside a file and not hardcode it as a string.

But where should you put a file such as about.txt? Of course, it would be convenient to simply place it with the rest of the program files inside a JAR file.

The `Class` class provides a useful service for locating resource files. Here are the necessary steps:

1. Get the `Class` object of the class that has a resource—for example, `ResourceTest.class`.
2. Some methods, such as the `getImage` method of the `ImageIcon` class, accept URLs that describe resource locations. Then you call:

    ```java
    URL url = cl.getResource("about.gif");
    ```

3. Otherwise, use the `getResourceAsStream` method to obtain an input stream for reading the data in the file.

The point is that the Java virtual machine knows how to locate a class, so it can then search for the associated resource in the same location. For example, suppose the `ResourceTest` class is in a package named `resources`. Then the `ResourceTest.class` file is located in a resources directory, and you place an icon file into the same directory.

Instead of placing a resource file inside the same directory as the class file, you can provide a relative or absolute path such as

```
data/about.txt
/corejava/title.txt
```

Automating the loading of files is all the resource loading feature does. There are no standard methods for interpreting the contents of resource files. Each program must have its own way of interpreting its resource files.

Another common application of resources is the internationalization of programs. Language-dependent strings, such as messages and user interface labels, are stored in resource files, with one file per language. The *internationalization API*, which is discussed in Chapter 7 of Volume II, supports a standard method for organizing and accessing these localization files.

Listing 5.13 is a program that demonstrates resource loading. (Do not worry about the code for reading text and displaying dialogs—we cover those details later.) Compile, build a JAR file, and execute it:

```bash
javac resource/ResourceTest.java
jar cvfe ResourceTest.jar resources.ResourceTest \
    resources/*.class resources/*.gif resources/data/*.txt corejava/*.txt
java -jar ResourceTest.jar
```

Move the JAR file to a different directory and run it again to check that the program reads the resource files from the JAR file, not from the current directory.

### Listing 5.13 resources/ResourceTest.java

```java
package resources;

import java.io.*;
import java.net.*;
import java.nio.charset.*;
import javax.swing.*;

/**
 * @version 1.5 2018-03-15
 * @author Cay Horstmann
 */
public class ResourceTest
{
    public static void main(String[] args) throws IOException
    {
        Class cl = ResourceTest.class;
        URL aboutURL = cl.getResource("about.gif");
        var icon = new ImageIcon(aboutURL);

        InputStream stream = cl.getResourceAsStream("data/about.txt");
        var about = new String(stream.readAllBytes(), "UTF-8");
```

Listing 5.14 shows you how to print out all information about a class. The program prompts you for the name of a class and writes out the signatures of all methods and constructors as well as the names of all instance fields of a class. For example, if you enter

```
    java.lang.Double
```

the program prints

```
    public class java.lang.Double extends java.lang.Number
    {
       public java.lang.Double(java.lang.String);
       public java.lang.Double(double);

       public int hashCode();
       public int compareTo(java.lang.Object);
       public int compareTo(java.lang.Double);
       public boolean equals(java.lang.Object);
       public java.lang.String toString();
       public static java.lang.String toString(double);
       public static java.lang.Double valueOf(java.lang.String);
       public static boolean isNaN(double);
       public boolean isNaN();
       public static boolean isInfinite(double);
       public boolean isInfinite();
       public byte byteValue();
       public short shortValue();
       public int intValue();
       public long longValue();
       public float floatValue();
       public double doubleValue();
       public static double parseDouble(java.lang.String);
       public static native long doubleToLongBits(double);
       public static native long doubleToRawLongBits(double);
       public static native double longBitsToDouble(long);

       public static final double POSITIVE_INFINITY;
       public static final double NEGATIVE_INFINITY;
       public static final double NaN;
       public static final double MAX_VALUE;
       public static final double MIN_VALUE;
       public static final java.lang.Class TYPE;
       private double value;
       private static final long serialVersionUID;
    }
```

What is remarkable about this program is that it can analyze any class that the Java interpreter can load, not just the classes that were available when the program was compiled. We will use this program in the next chapter to peek inside the inner classes that the Java compiler generates automatically.

### Listing 5.14 *(Continued)*

```java
48  public static void printConstructors(Class cl)
49  {
50     Constructor[] constructors = cl.getDeclaredConstructors();
51
52     for (Constructor c : constructors)
53     {
54        String name = c.getName();
55        System.out.print("  ");
56        String modifiers = Modifier.toString(c.getModifiers());
57        if (modifiers.length() > 0) System.out.print(modifiers + " ");
58        System.out.print(name + "(");
59
60        // print parameter types
61        Class[] paramTypes = c.getParameterTypes();
62        for (int j = 0; j < paramTypes.length; j++)
63        {
64           if (j > 0) System.out.print(", ");
65           System.out.print(paramTypes[j].getName());
66        }
67        System.out.println(");");
68     }
69  }
70
71  /**
72   * Prints all methods of a class
73   * @param cl a class
74   */
75  public static void printMethods(Class cl)
76  {
77     Method[] methods = cl.getDeclaredMethods();
78
79     for (Method m : methods)
80     {
81        Class retType = m.getReturnType();
82        String name = m.getName();
83
84        System.out.print("  ");
85        // print modifiers, return type and method name
86        String modifiers = Modifier.toString(m.getModifiers());
87        if (modifiers.length() > 0) System.out.print(modifiers + " ");
88        System.out.print(retType.getName() + " " + name + "(");
89
90        // print parameter types
91        Class[] paramTypes = m.getParameterTypes();
```
