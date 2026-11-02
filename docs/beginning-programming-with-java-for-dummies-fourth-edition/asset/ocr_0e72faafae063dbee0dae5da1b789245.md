# Comments

A comment is text that's outside the normal flow. In Figure 4-2, the words "A comment:" aren't part of the Suzanne sentence. Instead, these words are about the Suzanne sentence.

The same is true of comments in computer programs. The first five lines in Listing 4-1 form one big comment. The computer doesn't act on this comment. There are no instructions for the computer to perform inside this comment. Instead, the comment tells other programmers something about your code.

Comments are for your own benefit, too. Imagine that you set aside your code for a while and work on something else. When you return later to work on the code again, the comments help you remember what you were doing.

The Java programming language has three kinds of comments:

**Traditional comments:** The comment in Listing 4-1 is a traditional comment. The comment begins with /* and ends with */. Everything between the opening /* and the closing */ is for human eyes only. Nothing between /* and */ gets translated by the compiler.

The second, third, and fourth lines in Listing 4-1 have extra asterisks. I call them "extra" because these asterisks aren't required when you create a comment. They just make the comment look pretty. I include them in Listing 4-1 because, for some reason that I don't entirely understand, most Java programmers add these extra asterisks.

**End-of-line comments:** Here's some code with end-of-line comments:

```
class ThingsILike {        //Two things are missing
    public static void main(String args[]) {
        System.out.println("sleep"); // Missing from here
    }
}
```

An end-of-line comment starts with two slashes and goes to the end of a line of type.

You may hear programmers talk about commenting out certain parts of their code. When you're writing a program and something's not working correctly, it often helps to try removing some of the code. If nothing else, you find out what happens when that suspicious code is removed. Of course, you may not like what happens when the code is removed, so you don't want to delete the code completely. Instead, you turn your ordinary Java statements into comments. For example, turn System.out.println("Sleep"); into /* System.out.println("Sleep"); */. This keeps the Java compiler from seeing the code while you try to figure out what's wrong with your program.

![](bbox=[0.18, 0.78, 0.28, 0.92])