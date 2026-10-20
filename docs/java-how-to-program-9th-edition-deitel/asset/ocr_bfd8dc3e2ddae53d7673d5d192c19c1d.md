in its argument (the letter “J”) immediately after the last character that line 9 displays (the space character before the string’s closing double-quote character).

# Displaying Multiple Lines of Text with a Single Statement

A single statement can display multiple lines by using newline characters, which indicate to System.out’s print and println methods when to position the output cursor at the beginning of the next line in the command window. Like blank lines, space characters and tab characters, newline characters are white-space characters. The program in Fig. 2.4 outputs four lines of text, using newline characters to determine when to begin each new line. Most of the program is identical to those in Fig. 2.1 and Fig. 2.3.

```
1  // Fig. 2.4: Welcome3.java
2  // Printing multiple lines of text with a single statement.
3  
4  public class Welcome3
5  {
6      // main method begins execution of Java application
7      public static void main( String[] args )
8      {
9          System.out.println( "Welcome\nto\nJava\nProgramming!" );
10     } // end method main
11 } // end class Welcome3
```

![](bbox=[0.12, 0.5, 0.88, 0.6])

Fig. 2.4 | Printing multiple lines of text with a single statement.

Line 2

```
// Printing multiple lines of text with a single statement.
```

is a comment stating the program’s purpose. Line 4 begins the Welcome3 class declaration.

Line 9

```
System.out.println( "Welcome\nto\nJava\nProgramming!" );
```

displays four separate lines of text in the command window. Normally, the characters in a string are displayed exactly as they appear in the double quotes. Note, however, that the paired characters \ and n (repeated three times in the statement) do not appear on the screen. The backslash (\ ) is an escape character, which has special meaning to System.out’s print and println methods. When a backslash appears in a string, Java combines it with the next character to form an escape sequence. The escape sequence \n represents the newline character. When a newline character appears in a string being output with System.out, the newline character causes the screen’s output cursor to move to the beginning of the next line in the command window.

Figure 2.5 lists several common escape sequences and describes how they affect the display of characters in the command window. For the complete list of escape sequences, visit java.sun.com/docs/books/jls/third_edition/html/lexical.html#3.10.6.