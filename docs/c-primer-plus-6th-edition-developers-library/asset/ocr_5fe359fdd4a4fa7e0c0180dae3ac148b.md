# Summary

Many programs use getchar() to read input character-by-character. Typically, systems use line-buffered input, meaning that input is transmitted to the program when you press Enter. Pressing Enter also transmits a newline character that may require programming attention. ANSI C requires buffered input as the standard.

C features a family of functions, called the standard I/O package, that treats different file forms on different systems in a uniform manner. The getchar() and scanf() functions belong to this family. Both functions return the value EOF (defined in the stdio.h header) when they detect the end of a file. Unix systems enable you to simulate the end-of-file condition from the keyboard by pressing Ctrl+D at the beginning of a line; DOS systems use Ctrl+Z for the same purpose.

Many operating systems, including Unix and DOS, feature redirection, which enables you to use files instead of the keyboard and screen for input and output. Programs that read input up to EOF can then be used either with keyboard input and simulated end-of-file signals or with redirected files.

Interspersing calls to getchar() with calls to scanf() can cause problems when scanf() leaves a newline character in the input just before a call to getchar(). By being aware of this problem, however, you can program around it.

When you are writing a program, plan the user interface thoughtfully. Try to anticipate the sort of errors users are likely to make and then design your program to handle them.

# Review Questions

You’ll find answers to the review questions in Appendix A, “Answers to the Review Questions.”

+   1. putchar(getchar()) is a valid expression; what does it do? Is getchar(putchar()) also valid?

+   2. What would each of the following statements accomplish?
+   
+   a. putchar('H');
+   
+   b. putchar('\007');
+   
+   c. putchar('\n');
+   
+   d. putchar('\b');

+   3. Suppose you have an executable program named count that counts the characters in its input. Devise a command-line command using the count program to count the number of characters in the file essay and to store the result in a file named essayct.