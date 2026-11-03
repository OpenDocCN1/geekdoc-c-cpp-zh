+   IN THIS CHAPTER
+   » Using standard input and output
+   » Reading and writing characters
+   » Understanding getchar() and putchar()
+   » Exploring the char variable type
+   » Reading input with scanf()
+   » Grabbing strings with fgets()

# Chapter 7

# Input and Output

One of the basic functions, if not the basic function, of any computing device is input and output. The old I/O (say "eye oh") is also the goal of just about every program. Input is received and processed, and then output is generated. The processing is what makes the program useful. Otherwise, you'd have only input and output, which is essentially the same thing as plumbing.

# Character I/O

The simplest type of input and output takes place at the character level: One character goes in; one character comes out. Of course, getting to that point involves a wee bit of programming.

# Understanding input and output devices

The C language was born with the Unix operating system. As such, it follows many of the rules for that operating system with regard to input and output. Those rules are pretty solid:

+   » Input comes from the standard input device, stdin.
+   » Output is sent to the standard output device, stdout.