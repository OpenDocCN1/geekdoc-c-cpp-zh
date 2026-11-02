# A quick look at the Scanner

In this chapter, I advise you to ignore any of the meanings behind the lines `import java.util.Scanner` and `Scanner keyboard`, etc. Just paste these two lines mindlessly in your code and then move on.

Of course, you may not want to take my advice. You may not like ignoring things in your code. If you happen to be such a stubborn person, I have a few quick facts for you.

+   - **The word `Scanner` is defined in the Java API.**

A Scanner is something you can use for getting input.

This Scanner class belongs to Java versions 5.0 and higher. If you use version Java 1.4.2, you don't have access to the Scanner class. (You see an error marker when you type Listing 5-1.)

+   - **The words `System.in` are defined in the Java API.**

Taken together, the words `System.in` stand for the computer keyboard.

In later chapters, you see things like `new Scanner(new File("myData.txt"))`. In those chapters, I replace `System.in` with the words `new File("myData.txt")` because I'm not getting input from the keyboard. Instead, I'm getting input from a file on the computer's hard drive.

+   - **The word keyboard doesn't come from the Java API.**

The word keyboard is a Barry Burd creation. Instead of keyboard, you can use `readingThingie` (or any other name you want to use as long as you use the name consistently). So, if you want to be creative, you can write

```
Scanner readingThingie =
    new Scanner(System.in);
```

The revised Listing 5-1 (with `readingThingie` instead of `keyboard`) compiles and runs without a hitch.

+   - **The line `import java.util.Scanner` is an example of an import declaration.**

An optional import declaration allows you to abbreviate names in the rest of your program. You can remove the import declaration from Listing 5-1. But if you do, you must use the `Scanner` class's *fully qualified name* throughout your code. Here's how:

```
class EchoLine {

    public static void main
                         (String args[]) {

        java.util.Scanner keyboard
            = new java.util.Scanner
                         (System.in);

        System.out.println
            (keyboard.nextLine());

        keyboard.close();
    }
}
```