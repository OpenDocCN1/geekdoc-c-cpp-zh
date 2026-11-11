
**Figure 3.5** Detailed description of a `String` method

![](img/0e7b74ef51a065c077b42cd87b362288_120_0.png)

**TIP:**

If you have not already done so, download the JDK documentation, as described in [Chapter 2](#). Bookmark the `index.html` page of the documentation in your browser right now!

### 3.6.9 Building Strings

Occasionally, you need to build up strings from shorter strings, such as keystrokes or words from a file. It would be inefficient to use string concatenation for this purpose. Every time you concatenate strings, a new `String` object is constructed. This is time consuming and wastes memory. Using the `StringBuilder` class avoids this problem.

Follow these steps if you need to build a string from many small pieces. First, construct an empty string builder:

```java
StringBuilder builder = new StringBuilder();
```

Each time you need to add another part, call the `append` method.

```java
builder.append(ch);  // appends a single character
builder.append(str); // appends a string
```

When you are done building the string, call the `toString` method. You will get a string object with the character sequence contained in the builder.

```java
String completedString = builder.toString();
```

- inserts a code unit at position offset and returns this.
- `StringBuilder delete(int startIndex, int endIndex)` deletes the code units with offsets `startIndex` to `endIndex − 1` and returns this.
- `String toString()` returns a string with the same data as the builder or buffer contents.

### 3.6.10 Text Blocks

The text block feature, added in Java 15, makes it easy to provide string literals that span multiple lines. A text block starts with `"""`, followed by a line feed. The block ends with another `"""`.

```java
String greeting = """
Hello
World
""";
```

A text block is easier to read and write than the equivalent string literal:

```
"Hello\nWorld\n"
```

This string contains two `\n`: one after Hello and one after World. The newline after the opening `"""` is not included in the string literal.

If you don’t want a newline after the last line, put the closing `"""` immediately after the last character:

```java
String prompt = """
Hello, my name is Hal.
Please enter your name: """;
```

Text blocks are particularly suited for including code in some other language, such as SQL or HTML. You can just paste it between the triple quotes:

```java
String html = """
<div class="Warning">
    Beware of those who say "Hello" to the world
</div>
""";
```

Note that you don’t have to escape the quotation marks. There are just two situations where you need to escape them:

- If the text block *ends* in a quotation mark
- If the text block contains a sequence of three or more quotation marks

Unfortunately, you still need to escape all backslashes.

All escape sequences from regular strings work the same way in text blocks.

There is one escape sequence that only works in text blocks. A \ directly before the end of a line joins this line and the next. For example,

```java
"""
Hello, my name is Hal. \
Please enter your name: """;
```

is the same as

```
"Hello, my name is Hal. Please enter your name: "
```

Line endings are normalized by removing trailing whitespace and changing any Windows line endings (`\r\n`) to simple newlines (`\n`). In the unlikely case that you need to preserve trailing spaces, turn the last one into a `\s` escape.

The story is more complex for leading white space. Consider a typical variable declaration that is indented from the left margin. You can indent the text block as well:

```java
String html = """
    <div class="Warning">
        Beware of those who say "Hello" to the world
    </div>
""";
```

The indentation that is common to all lines in the text block is subtracted. The actual string is

```
"<div class=\"Warning\">\n    Beware of those who say \"Hello\" to the world\n</div>\n"
```

Note that there are no indentations in the first and third line.

Your IDE may cheerfully offer to indent all text blocks, using only tabs, only spaces, or an appropriate mix.

Java wisely does not prescribe the width of a tab. The white space prefix has to match *exactly* for all lines in the text block.

Entirely blank lines are not considered in the indentation removal process. However, the white space before the closing `"""` is significant. Be sure to indent to the end of the white space that you want to have stripped.

![](img/0e7b74ef51a065c077b42cd87b362288_124_0.png)

**CAUTION:**

Be careful about mixed tabs and spaces in the common prefix of an indented text block. An overlooked space can easily yield a wrongly indented string.

![](img/0e7b74ef51a065c077b42cd87b362288_125_0.png)

**TIP:**

If a text block contains code that isn’t Java, you may actually prefer to place it at the left margin. It stands out from the Java code, and you have more room for long lines.

## 3.7 Input and Output

To make our example programs more interesting, we want to accept input and properly format the program output. Of course, modern programs use a GUI for collecting user input. However, programming such an interface requires more tools and techniques than we have at our disposal at this time. Our first order of business is to become more familiar with the Java programming language, so we use the humble console for input and output.

### 3.7.1 Reading Input

You saw that it is easy to print output to the “standard output stream” (that is, the console window) just by calling `System.out.println`. Reading from the “standard input stream” `System.in` isn’t quite as simple. To read console input, you first construct a `Scanner` that is attached to `System.in`:

```java
Scanner in = new Scanner(System.in);
```

(Constructors and the new operator are discussed in detail in [Chapter 4](#chapter-4).)

Now you can use the various methods of the `Scanner` class to read input. For example, the `nextLine` method reads a line of input.

```java
System.out.print("What is your name? ");
String name = in.nextLine();
```

Here, we use the `nextLine` method because the input might contain spaces. To read a single word (delimited by whitespace), call

```java
String firstName = in.next();
```

To read an integer, use the `nextInt` method.

```java
System.out.print("How old are you? ");
int age = in.nextInt();
```

Similarly, the `nextDouble` method reads the next floating-point number.

The program in [Listing 3.2](#) asks for the user’s name and age and then prints a message like

```
Hello, Cay. Next year, you'll be 57
```

Finally, note the line

```
import java.util.*;
```

at the beginning of the program. The `Scanner` class is defined in the `java.util` package. Whenever you use a class that is not defined in the basic `java.lang` package, you need to use an import directive. Packages and import directives are covered in more detail in [Chapter 4](#).

**Listing 3.2** `InputTest/InputTest.java`

```java
1   import java.util.*;
2
3   /**
4    * This program demonstrates console input.
5    * @version 1.10 2004-02-10
6    * @author Cay Horstmann
7    */
8   public class InputTest
9   {
10      public static void main(String[] args)
11      {
12      Scanner in = new Scanner(System.in);

14      // get first input
15      System.out.print("What is your name? ");
16      String name = in.nextLine();

18      // get second input
19      System.out.print("How old are you? ");
20      int age = in.nextInt();

22      // display output on console
23      System.out.println("Hello, " + name + ". Next year, you'll be " + (age + 1));
24      }
25 }
```

> **NOTE:**
>
> The Scanner class is not suitable for reading a password from a console since the input is plainly visible to anyone. Use the Console class for this purpose. To read a password, use the following code:

![](img/0e7b74ef51a065c077b42cd87b362288_127_0.png)

```java
Console cons = System.console();
String username = cons.readLine("User name: ");
char[] passwd = cons.readPassword("Password: ");
```

For security reasons, the password is returned in an array of characters rather than a string. After you are done processing the password, you should immediately overwrite the array elements with a filler value. (Array processing is discussed in Section 3.10, “Arrays,” on p. 109.)

Input processing with a Console object is not as convenient as with a Scanner. You must read the input a line at a time. There are no methods for reading individual words or numbers.
