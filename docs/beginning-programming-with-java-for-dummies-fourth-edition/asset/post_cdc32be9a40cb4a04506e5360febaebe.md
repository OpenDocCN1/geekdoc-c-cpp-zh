
In English, you write all the way across one line and then you wrap your text to the start of the next line. In programming, you seldom work this way. Instead, the code's punctuation guides the indenting of certain lines. The indentation shows which parts of the program are subordinate to which other parts. It's as though, in English, you wrote Suzanne's sentence like this:

> Suzanne says "eh" because
> 
>     as you know
> 
> she lives in Canada.

The diagrams in Figures 4-3 and 4-4 show you how parts of the ThingsILike program are contained inside other parts. Notice how a pair of curly braces acts like a box. To make the program's structure visible at a glance, you indent all the stuff inside of each box.

Figure 4-3: A pair of curly braces acts like a box.

```
class ThingsILike {
    public static void main(String args[]) {
        System.out.println("Chocolate, royalties, sleep");
    }
}
```

Figure 4-4: The ideas in a computer program are nested inside one another.

Here's a Java class named ThingsILike:<br>
Here's the main starting point for the instructions:<br>
Display Chocolate, royalties, sleep on the screen.

![](img/6d9dcff12e52b997f3ad31445b712549_101_0.png)

I can't emphasize this point enough. If you don't indent your code or if you indent but you don't do it carefully, then your code still compiles and runs correctly. But this successful run gives you a false sense of confidence. The minute you try to update some poorly indented code, you become hopelessly confused. So take my advice: Keep your code carefully indented at every step in the process. Make your indentation precise, whether you're scratching out a quick test program or writing code for a billionaire customer.

![](img/6d9dcff12e52b997f3ad31445b712549_101_1.png)

Eclipse can indent your code automatically for you. Select the .java file whose code you want to indent. Then, in Eclipse's main menu, choose Source->Format. Eclipse rearranges your lines in the editor, indenting things that should be indented and generally making your code look good.

## Comments

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

![](img/6d9dcff12e52b997f3ad31445b712549_102_0.png)

**Javadoc comments:** A special Javadoc comment is any traditional comment that begins with an extra asterisk.

```
/**
 * Print a String and then terminate the line.
 */
```

This is a cool Java feature. The software that you can download from java.sun.com includes a little program called javadoc. The javadoc program looks for these special comments in your code. The program uses these comments to create a brand new web page — a customized documentation page for your code. To find out more about turning Javadoc comments into web pages, visit this book's website (http://allmycode.com/BeginProg).

## Understanding a Simple Java Program

The following sections present, explain, analyze, dissect, and otherwise demystify the Java program in Listing 4-1.

### What is a method?

You're working as an auto mechanic in an upscale garage. Your boss, who's always in a hurry and has a habit of running words together, says, "FixTheAlternator." Mentally, you run through a list of tasks. "Drive the car into the bay, lift the hood, get a wrench, loosen the alternator belt," and so on. Three things are going on here:

- **You have a name for the thing you're supposed to do.** The name is FixTheAlternator.
- **In your mind, you have a list of tasks associated with the name FixTheAlternator.** The list includes "Drive the car into the bay, lift the hood, get a wrench, loosen the alternator belt," and so on.
- **You have a grumpy boss who's telling you to do all this work.** Your boss gets you working by saying, "FixTheAlternator." In other words, your boss gets you working by saying the name of the thing you're supposed to do.

In this scenario, using the word method wouldn't be a big stretch. You have a method for doing something with an alternator. Your boss calls that method into action, and you respond by doing all the things in the list of instructions that you've associated with the method.

### Java methods

If you believe all that stuff in the preceding section, then you're ready to read about Java methods. In Java, a method is a list of things to do. Every method has a name, and you tell the computer to do the things in the list by using the method's name in your program.

I've never written a program to get a robot to fix an alternator. But, if I were to, the program might include a method named FixTheAlternator. The list of instructions in my FixTheAlternator method would look something like the text in Listing 4-2.

**Listing 4-2: A Method Declaration**

```
void FixTheAlternator() {
    DriveInto(car, bay);
    Lift(hood);
    Get(wrench);
    Loosen(alternatorBelt);
    ...
}
```

Somewhere else in my Java code (somewhere outside of Listing 4-2), I need an instruction to call my FixTheAlternator method into action. The instruction to call the FixTheAlternator method into action may look like the line in Listing 4-3.

**Listing 4-3: Calling a Method**

```
FixTheAlternator(junkyOldFord);
```

![](img/6d9dcff12e52b997f3ad31445b712549_104_0.png)

Don't scrutinize Listings 4-2 and 4-3 too carefully. All the lines of code in Listings 4-2 and 4-3 are fakes! I made up this code so that it looks a lot like real Java code, but it's not real. What's more important, the code in Listings 4-2 and 4-3 isn't meant to illustrate all the rules about Java. So if you have a grain of salt handy, take it with Listings 4-2 and 4-3.

![](img/6d9dcff12e52b997f3ad31445b712549_104_1.png)

Almost every computer programming language has something akin to Java's methods. If you've worked with other languages, you may remember things like subprograms, procedures, functions, subroutines, Sub procedures, or PERFORM statements. Whatever you call it in your favorite programming language, a method is a bunch of instructions collected together and given a new name.
