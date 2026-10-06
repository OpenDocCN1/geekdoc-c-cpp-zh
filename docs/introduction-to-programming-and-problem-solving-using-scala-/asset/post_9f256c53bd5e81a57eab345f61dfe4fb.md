
# Scala Basics

There are three ways in which the scala command can be used. If you just type scala and press enter you will be dropped into the Scala REPL (Read-Execute-Print Loop). It is an environment where you can use Scala commands and immediately see their values. This is how we will start interacting with Scala, and it is something that we will come back to throughout the book because it allows us to easily experiment and play around with the language. The fact that it gives us immediate feedback is also quite helpful.

To see how this works, at the prompt, type scala and then press enter. It should print out some information for you, telling you that you can get help by typing :help. It will give you a prompt of the form scala>. You are now in the Scala REPL. If you type :help you will see a number of other commands you could get that begin with a colon. At this time the only one that is significant to us is :quit which we use when we are done with the REPL and to go back to the normal command prompt.

It is customary for the first program in a language to be Hello World. So not to break with tradition

```
println("Hello, World!")
```

If you do this then the next line prints out "Hello, World!". This exercise is less exciting in the REPL because it always prints the values of things, and it is a reasonable thing to start with. It is worth asking what is println function in Scala that tells it to print something to standard output and follow that with a newline character to go to the next line. In this case, the thing that was printed was the string "Hello, World". You can print other things if you wish. One of the advantages of the REPL is that you can play around. Go ahead and try other things to see what happens.

The second usage of the scala command is to run small programs as scripts. The term script is generally used to refer to short programs that perform specific tasks. There are languages that are designed to work in this type of usage, and are often called scripting languages. The design of Scala makes it easy to use as scripting language. Unlike most scripting languages, Scala also has many features that make it ideal for developing large software projects. To use Scala for scripting, simply type in a little program to a text file that ends with ".scala" and run it by putting the file name after the scala command on the command line. You could edit a file Hello.scala and add the line of code from above to it. After you have saved the file, go to the command line and enter "scala Hello.scala" to see it run.

# Expressions, Types, and Basic Math

All programming languages are built from certain fundamental parts. In English we put together words into phrases and then combine phrases into sentences. These sentences can be put together to make paragraphs. To help you understand programming, we make analogies between standard English and programming languages. These analogies are

> 2 You will find more information about the other escape characters in section 2.8
> 3 It is not technically required that your file ends with ".scala", but there are at least two good reasons you should do this. First, humans benefit from standard file extensions because they have meaning and make it easier to keep track of things. Second, some tools treat things differently based on extensions. For example, some text editors will color code differently based on the file extension.

# Introduction to Programming and Problem-Solving Using Scala

not perfect. You cannot push them too far. However, they should help you to organize your thinking in the process. Later on, when your understanding of programming is more mature, you can dispense with these analogies as you will be able to think about programming languages in your own terms.

The smallest piece of a programming language that has meaning is called a TOKEN. A token is like a word or punctuation in English. If you break up a token, you change the meaning of that piece, just like breaking up a word is likely to result in something that is no longer a word and does not have any meaning at all. Indeed, many of the tokens in Scala are words. Other tokens are symbols like punctuation. Let's consider the "Hello, World" example from the previous section.

```
println("Hello, World!")
```

When you think of putting words together, you probably think of building sentences with them. A sentence is a group of words that stands on its own in English. The equivalent of a sentence in Scala, and most programming languages, is the STATEMENT. A statement is a complete and coherent instruction that we give the computer. When you are entering "commands" into the REPL, they are processed as full statements. If you enter something that is not a complete statement in the REPL, instead of the normal prompt, you will see a vertical bar on the next line that you need to continue the statement. The command listed above is a complete statement which is why it worked the way it did.

Note that statement ends with a semicolon. In English we use for ending sentences with a period, question mark, or exclamation point. Scala follows many other programming languages in semicolons. Scala also does something called semicolon inference. Simply put, if you end a line in such a way that a semicolon makes sense, Scala will put one for you. As a result of this, our print statement will work as well as without the semicolon.

```
println("Hello, World!")
```

You should try entering this into the REPL to verify that it works. Thanks to the semicolon inference in Scala, you will rarely have to put semicolons in code. One of the few times they will really be needed when we want to put two statements on a single line for formatting reasons.

While you think of building sentences from words in English, the reality is that you put words together and join them into phrases. The equivalent of a phrase is the EXPRESSION. Expressions have a far more significant impact on programming languages than phrases, or at least the programmers need to be more cognizant of expressions than English writers have to be. An expression is a group of tokens in the language that has a value and a TYPE. For example, 2 + 2 is an expression which evaluate to 4 and has an integer type.

Just like some phrases are made from a single word, some tokens represent things that have values on their, and, as such, expressions are LITERALS. The most basic of what we are our sample line was not only a statement, but also an expression. In Scala, any valid expression can be used as a statement, but some statements are not expressions. The "Hello, World!" of our statement was also an expression. It is something called a literal which we will learn more about in section 2.4.

Let us take a bit of time to explore these concepts in the REPL. Run the scala command

> Type is a construct that specifies a set of values and the operations that can be performed on them. Common types include numeric integer, floating-point, character, and boolean.

# Scala Basics 21

without any arguments. This will put you the REPL with a prompt of scala>. In the last chapter I typed in a line that told Scala to print something. This was made from more than one. We want to start simpler here. Type in a number, like 5, followed by a semicolon and hit enter. You would see something like this:

```
scala> 5;
res0: Int = 5
```

The first line is what you typed at the prompt. The second line is what the Scala REPL printed out as an answer. Recall that REPL stands for Read-Evaluate-Loop. When you type something in, the REPL implies that this happens over and over. After it evaluates it and prints the result, you should have given it a new prompt.

So what does second line mean? The REPL evaluated the statement that you input. In this case, the statement is an expression followed by a semicolon and the REPL was printing the value of the expression you entered. As mentioned above, the REPL needs you to type in full statements so that it can evaluate it. In this case, we typed a very simple statement that has an expression called NUMERIC LITERAL by a semicolon. This semicolon will be inferred if you do not add it in. We will take advantage of that and leave them out.

The end of the output gives us the value of the expression which is, surprisingly. What about the stuff before that? What does res0 mean? The res0 part is a number. It is short for "result". When you type an expression as a statement in the REPL, it does not just evaluate it, it gives you a name that you can refer to. The name is now associated with the 5 in this part of the REPL. We will come back to this later. Colors are used in Scala to separate things from their types. We will see a lot more of this through the book, but what matters most to us now is the type, Int. This is the type that Scala uses for basic numeric integers. An integer can be either a positive or negative number. 

Most of the times the result will not be all that, but if you push things far enough you might get a surprise or two.

What happens if you type in a number that is not an integer? For example, what if you type in 5.6? Try it, and you would get something like this:

```
scala> 5.6
res1: Double = 5.6
```

We have a different name now because this is a new result. We also get a different type. Instead of Int, Scala now tells us the type is Double. In Double, the Scala uses by default for any non-integer values. If a value is technically an integer, if it includes a decimal point, Scala will interpret it as a Double. You can type in 5.0 to see this in. Trying in some other numeric values that should have a Double as the type. What happens. Anyway, the results will be fairly mundane. Double literals also use scientific notation by putting the letter e between a number and the power of ten it is multiplied by. So 5e3 means 5 * 10^3

So far, all of the expressions we have typed in been single tokens. We will build some more complex expressions. We will begin by doing basic mathematical operations. Try typing in "5+6":

```
scala> 5+6
res2: Int = 11
```
