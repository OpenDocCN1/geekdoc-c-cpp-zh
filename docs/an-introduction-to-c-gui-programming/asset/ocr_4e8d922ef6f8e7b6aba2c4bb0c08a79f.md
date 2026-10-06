This calls the gcc C compiler with the option -o myprog, which tells it to create an executable output file called myprog and to use hello.c as the input source code
If you entered your C code correctly (did you make sure the semicolon was there?), this should take a second or so and then return you to the command line. There should now be a file in the current directory called myprog – try running it by typing:

./myprog

Et voilà! You should now have

Hello World!

written in the terminal

```
File Edit Tabs Help
pi@raspberry:~ $ gcc -o myprog hello.c
pi@raspberry:~ $ ./myprog
Hello World!
pi@raspberry:~ $ |
```

# RUNNING YOUR PROGRAM

That's your first C program written, compiled, and run. In the next chapter, we'll start C for something a bit more useful!