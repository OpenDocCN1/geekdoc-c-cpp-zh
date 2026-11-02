
**Javadoc comments:** A special Javadoc comment is any traditional comment that begins with an extra asterisk.

```
/**
 * Print a String and then terminate the line.
 */
```

This is a cool Java feature. The software that you can download from java.sun.com includes a little program called javadoc. The javadoc program looks for these special comments in your code. The program uses these comments to create a brand new web page — a customized documentation page for your code. To find out more about turning Javadoc comments into web pages, visit this book's website (http://allmycode.com/BeginProg).

## Understanding a Simple Java Program

The following sections present, explain, analyze, dissect, and otherwise demystify the Java program in Listing 4-1.

## What is a method?

You're working as an auto mechanic in an upscale garage. Your boss, who's always in a hurry and has a habit of running words together, says, "FixTheAlternator." Mentally, you run through a list of tasks. "Drive the car into the bay, lift the hood, get a wrench, loosen the alternator belt," and so on. Three things are going on here:

- **You have a name for the thing you're supposed to do.** The name is FixTheAlternator.
- **In your mind, you have a list of tasks associated with the name FixTheAlternator.** The list includes "Drive the car into the bay, lift the hood, get a wrench, loosen the alternator belt," and so on.
- **You have a grumpy boss who's telling you to do all this work.** Your boss gets you working by saying, "FixTheAlternator." In other words, your boss gets you working by saying the name of the thing you're supposed to do.

In this scenario, using the word method wouldn't be a big stretch. You have a method for doing something with an alternator. Your boss calls that method into action, and you respond by doing all the things in the list of instructions that you've associated with the method.

## Java methods

If you believe all that stuff in the preceding section, then you're ready to read about Java methods. In Java, a method is a list of things to do. Every method has a name, and you tell the computer to do the things in the list by using the method's name in your program.

I've never written a program to get a robot to fix an alternator. But, if I were to, the program might include a method named FixTheAlternator. The list of instructions in my FixTheAlternator method would look something like the text in Listing 4-2.

### Listing 4-2: A Method Declaration

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

### Listing 4-3: Calling a Method

```
FixTheAlternator(junkyOldFord);
```

![](img/bf4858233d2b2a32ff4e3991860526b3_104_0.png)

Don't scrutinize Listings 4-2 and 4-3 too carefully. All the lines of code in Listings 4-2 and 4-3 are fakes! I made up this code so that it looks a lot like real Java code, but it's not real. What's more important, the code in Listings 4-2 and 4-3 isn't meant to illustrate all the rules about Java. So if you have a grain of salt handy, take it with Listings 4-2 and 4-3.

![](img/bf4858233d2b2a32ff4e3991860526b3_104_1.png)

Almost every computer programming language has something akin to Java's methods. If you've worked with other languages, you may remember things like subprograms, procedures, functions, subroutines, Sub procedures, or PERFORM statements. Whatever you call it in your favorite programming language, a method is a bunch of instructions collected together and given a new name.

## The declaration, the header, and the call

If you have a basic understanding of what a method is and how it works (see preceding section), you can dig a little deeper into some useful terminology:

- If I'm being lazy, I refer to the code in Listing 4-2 as a *method*. If I'm not being lazy, I refer to this code as a *method declaration*.
- The *method declaration* in Listing 4-2 has two parts. The first line (the part with the name FixTheAlternator in it, up to but not including the open curly brace) is called a *method header*. The rest of Listing 4-2 (the part surrounded by curly braces) is a *method body*.
- The term *method declaration* distinguishes the list of instructions in Listing 4-2 from the instruction in Listing 4-3, which is known as a *method call*.

For a handy illustration of all the method terminology, see Figure 4-5.

**Figure 4-5:** The terminology describing methods.

![](img/bf4858233d2b2a32ff4e3991860526b3_105_0.png)

A method's header and body are like an entry in a dictionary. An entry doesn't really use the word that it defines. Instead, an entry tells you what happens if and when you use the word.

> chocolate (choc-o-late) n. 1. The most habit-forming substance on earth. 2. Something you pay for with money from royalties. 3. The most important nutritional element in a person's diet.
>
> FixTheAlternator() Drive the car into the bay, lift the hood, get the wrench, loosen the alternator belt, and then eat some chocolate.

In contrast, a method call is like the use of a word in a sentence. A method call sets some code in motion.

> "I want some chocolate, or I'll throw a fit."
>
> "FixTheAlternator on that junkyOldFord."

![](img/bf4858233d2b2a32ff4e3991860526b3_106_0.png)

A method's declaration tells the computer what will happen if you call the method into action. A method call (a separate piece of code) tells the computer to actually call the method into action. A method's declaration and the method's call tend to be in different parts of the Java program.

## The main method in a program

In Listing 4-1, the bulk of the code is the declaration of a method named main. (Just look for the word main in the code's method header.) For now, don't worry about the other words in the method header — the words public, static, void, String, and args. I explain these words (on a need-to-know basis) in the next several chapters.

Like any Java method, the main method is a recipe:

```
How to make biscuits:
Preheat the oven.
Roll the dough.
Bake the rolled dough.
```

```
How to follow the main instructions in the ThingsILike code:
Display Chocolate, royalties, sleep on the screen.
```

The word main plays a special role in Java. In particular, you never write code that explicitly calls a main method into action. The word main is the name of the method that is called into action automatically when the program begins running.

When the ThingsILike program runs, the computer automatically finds the program's main method and executes any instructions inside the method's body. In the ThingsILike program, the main method's body has only one instruction. That instruction tells the computer to print Chocolate, royalties, sleep on the screen.

![](img/bf4858233d2b2a32ff4e3991860526b3_107_0.png)

None of the instructions in a method are executed until the method is called into action. But if you give a method the name main, that method is called into action automatically.

## How you finally tell the computer to do something

Buried deep in the heart of Listing 4-1 is the single line that actually issues a direct instruction to the computer. The line

```
System.out.println("Chocolate, royalties, sleep");
```

tells the computer to display the words Chocolate, royalties, sleep. (If you use Eclipse, the computer displays Chocolate, royalties, sleep in the Console view.) I can describe this line of code in at least two different ways:

- **It's a statement.** In Java, a direct instruction that tells the computer to do something is called a statement. The statement in Listing 4-1 tells the computer to display some text. The statements in other programs may tell the computer to put 7 in a certain memory location or make a window appear on the screen. The statements in computer programs do all kinds of things.
- **It's a method call.** In the "What is a method?" section, earlier in this chapter, I describe something named a "method call." The statement `FixTheAlternator(junkyOldFord);` is an example of a method call, and so is `System.out.println("Chocolate, royalties, sleep");`

```
FixTheAlternator(junkyOldFord);
```

```
System.out.println("Chocolate, royalties, sleep");
```

Java has many different kinds of statements. A method call is just one kind.
