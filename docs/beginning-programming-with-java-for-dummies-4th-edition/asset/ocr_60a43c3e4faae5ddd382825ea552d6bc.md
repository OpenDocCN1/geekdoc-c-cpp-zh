# 6. Look for versions of Java in the User tab and the System tab of the Java Runtime Environment Settings window.

Figure 2-7 shows the User tab of the Java Runtime Environment Settings window. According to the figure, the computer runs Java 1.8. (Java's close friends call this version "Java 8.")

# On Linux

To check your Java installation (or your lack of Java) on a Linux computer, do the following:

+   1. **Poke around among the desktop's menus for something named Terminal (also known as Konsole).**
+   
+   A Terminal window opens (usually with plain white text on a plain black background).
+   
+   2. **In the Terminal window, type the following text and then press Enter:** `java -version.`
+   
+   On my Linux computer, the Terminal window responds with the following text:

```
java version 1.8.0_1
```

If your computer responds with the number 1.8.0 or higher, you can pop open the champagne and look forward to some good times running this book's examples. If the version number is 1.5 or greater, you can run many, but not all, of this book's examples. If your computer responds with something like command not found, most likely, Java isn't installed on your computer.

# Setting Up the Eclipse Integrated Development Environment

In the previous sections, you get all the tools your computer needs for processing Java programs. This section is different. In this section, you get the tool that you need for composing and testing your Java programs. You get Eclipse — an integrated development environment for Java.

An integrated development environment (IDE) is a program that provides tools to help you create software easily and efficiently. You can create Java programs without an IDE, but the time and effort you save using an IDE makes the IDE worthwhile. (Some hard-core programmers disagree with me, but that's another matter.)