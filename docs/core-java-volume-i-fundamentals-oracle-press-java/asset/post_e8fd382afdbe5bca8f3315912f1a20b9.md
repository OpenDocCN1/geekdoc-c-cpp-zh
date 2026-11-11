
Depending on the operating system configuration, users may even be able to launch the application by double-clicking the JAR file icon. Here are behaviors for various operating systems:

- On Windows, the Java runtime installer creates a file association for the “.jar” extension that launches the file with the `javaw -jar` command. (Unlike the `java` command, the `javaw` command doesn’t open a shell window.)
- On Mac OS X, the operating system recognizes the “.jar” file extension and executes the Java program when you double-click a JAR file.

However, a Java program in a JAR file does not have the same feel as a native application. On Windows, you can use third-party wrapper utilities that turn JAR files into Windows executables. A wrapper is a Windows program with the familiar `.exe` extension that locates and launches the Java virtual machine (JVM) or tells the user what to do when no JVM is found. There are a number of commercial and open source products, such as Launch4J (http://launch4j.sourceforge.net) and IzPack (http://izpack.org).

### 4.9.4 Multi-Release JAR Files

With the introduction of modules and strong encapsulation of packages, some previously accessible internal APIs are no longer available. This may require library providers to distribute different code for different Java versions. Java 9 introduces *multi-release JARs* for this purpose.

For backwards compatibility, version-specific class files are placed in the

As of Java 9, the `-d` option creates the directory if it doesn't exist.

The `--release` flag is also new with Java 9. In older versions, you needed to use the `-source`, `-target`, and `-bootclasspath` flags. The JDK now ships with symbol files for two prior versions of the API. In Java 9, you can compile with `--release` set to 9, 8, or 7.

Multi-release JARs are not intended for different versions of a program or library. The public API of all classes should be the same for both releases. The sole purpose of multi-release JARs is to enable a particular version of your program or library to work with multiple JDK releases. If you add functionality or change an API, you should provide a new version of the JAR instead.

> **NOTE:**
>
> Tools such as `javap` are not retrofitted to handle multi-release JAR files. If you call
>
> ```text
> javap -classpath MyProgram.jar Application.class
> ```
>
> you get the base version of the class (which, after all, is supposed to have the same public API as the newer version). If you must look at the newer version, call
>
> ```text
> javap -classpath MyProgram.jar!/META-INF/versions/9/Application.class
> ```

### 4.9.5 A Note about Command-Line Options

The options of commands in the Java Development Kit have traditionally used single dashes followed by multiletter option names, such as

Arguments of single-letter options can be separated by whitespace or directly follow the option:

```text
javac -p moduledir . . .
```

or

```text
javac -pmoduledir . . .
```

![](img/0e7b74ef51a065c077b42cd87b362288_305_0.png)

> **CAUTION:**
>
> The latter doesn’t currently work, and it also seems like a bad idea in general. Why invite conflicts with legacy options if the module directory happens to be a parameter or processor?

Single-letter options without arguments can be grouped together:

```text
jar -cvf MyProgram.jar -e mypackage.MyProgram */*.class
```

![](img/0e7b74ef51a065c077b42cd87b362288_305_1.png)

> **CAUTION:**
>
> That doesn’t currently work, and it is bound to lead to confusion. Suppose `javac` gains a `-c` option. Does `javac -cp` mean `javac -c -p`, or does the legacy `-cp` take precedence?

This has created a muddle that will hopefully get cleaned up over time. As much as I’d like to move away from the archaic jar options, it seems best to wait until the dust has settled. But if you want to be thoroughly modern, you can safely use the long options of the jar command:

```text
jar --create --verbose --file jarFileName file1 file2 . . .
```

Single-letter options also work if you don’t group them:

```text
jar -c -v -f jarFileName file1 file2 . . .
```

## 4.10 Documentation Comments

The JDK contains a very useful tool, called `javadoc`, that generates HTML documentation from your source files. In fact, the online API documentation described in Chapter 3 is simply the result of running `javadoc` on the source code of the standard Java library.

If you add comments that start with the special delimiter `/**` to your source code, you too can easily produce professional-looking documentation. This is a very nice approach because it lets you keep your code and documentation in one place. If you put your documentation into a separate file, then, as you probably know, the code and comments tend to diverge over time. When documentation comments are in the same file as the source code, it is an easy matter to update both and run `javadoc` again.

### 4.10.1 Comment Insertion

The `javadoc` utility extracts information for the following items:

- Modules
- Packages
- Public classes and interfaces
- Public and protected fields
- Public and protected constructors and methods

Protected features are introduced in Chapter 5, interfaces in Chapter 6, and modules in Chapter 9 of Volume II.

```java
/**
 * A {@code Card} object represents a playing card, such
 * as "Queen of Hearts". A card has a suit (Diamond, Heart,
 * Spade or Club) and a value (1 = Ace, 2 . . . 10, 11 = Jack,
 * 12 = Queen, 13 = King)
 */
public class Card
{
   . . .
}
```

**NOTE:**

There is no need to add an `*` in front of every line. For example, the following comment is equally valid:

```java
/**
   A <code>Card</code> object represents a playing card, such
   as "Queen of Hearts". A card has a suit (Diamond, Heart,
   Spade or Club) and a value (1 = Ace, 2 . . . 10, 11 = Jack,
   12 = Queen, 13 = King).
*/
```

However, most IDEs supply the asterisks automatically and rearrange them when the line breaks change.

### 4.10.3 Method Comments

Each method comment must immediately precede the method that it describes. In addition to the general-purpose tags, you can use the following tags:

- `@param` *variable description*
  
  This tag adds an entry to the “parameters” section of the current method. The description can span multiple lines and can use HTML tags. All `@param` tags for one method must be kept together.
- `@return` *description*
  
  This tag adds a “returns” section to the current method. The description can span multiple lines and can use HTML tags.
- `@throws` *class description*
  
  This tag adds a note that this method may throw an exception. Exceptions are the topic of Chapter 7.

Here is an example of a method comment:

```java
/**
 * Raises the salary of an employee.
 * @param byPercent the percentage by which to raise the salary (e.g., 10 means 10%)
 * @return  the amount of the raise
 */
public double raiseSalary(double byPercent)
{
    double raise = salary * byPercent / 100;
    salary += raise;
    return raise;
}
```

### 4.10.4 Field Comments

You only need to document public fields—generally that means static constants. For example:

```java
/**
 * The "Hearts" card suit
 */
public static final int HEARTS = 1;
```

### 4.10.5 General Comments

The tag `@since` *text* makes a “since” entry. The *text* can be any description of the version that introduced this feature. For example, `@since 1.7.1`.

The following tags can be used in class documentation comments:

- `@author` *name*
  
  This tag makes an “author” entry. You can have multiple `@author` tags, one for each author. Don’t feel compelled to use this tag—your version control system does a more thorough job tracking authorship.
- `@version` *text*
  
  This tag makes a “version” entry. The *text* can be any description of the current version.

You can use hyperlinks to other relevant parts of the javadoc documentation, or to external documents, with the `@see` and `@link` tags.

The tag `@see` *reference* adds a hyperlink in the “see also” section. It can be used with both classes and methods. Here, *reference* can be one of the following:

```text
package.class#feature label
<a href="..">label</a>
"text"
```

The first case is the most useful. You supply the name of a class, method, or variable, and javadoc inserts a hyperlink to the documentation. For example,

`@see com.horstmann.corejava.Employee#raiseSalary(double)`

makes a link to the `raiseSalary(double)` method in the `com.horstmann.corejava.Employee` class. You can omit the name of the package, or both the package and class names. Then, the feature will be located in the current package or class. Note that you must use a `#`, not a period, to separate the class from the method or variable name. The Java
