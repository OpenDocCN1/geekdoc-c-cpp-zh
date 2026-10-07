
## Chapter 2 Programming in Objective-C

If you make mistakes in your program, along the way you'll see errors denoted as red stop signs containing exclamation points—these are known as fatal errors and you can't run your program without correcting them. Warnings are depicted by yellow triangles containing exclamation points—you can still run your program with them, but in general you should examine and correct them. After running the program with all the errors, the lower pane will display the output from your program and should look similar to Figure 2.9. Don't worry about the verbose messages that appear. The output line you're interested in is the one you see below.

![](img/9a03a17dbf1900dce936c9665ab15c26_27_0.png)

Figure 2.9 Xcode Debug output

You are now done with the procedural part of compiling and running your first program with Xcode (whew!). The following summarizes the steps involved in creating a new program with Xcode:

- 1. Start the Xcode application.
- 2. If this is a new project, select File, New, New Project... or choose Create a New Xcode Project from the startup screen.
- 3. For the type of application, select Application, Command Line Tool, and click Next.
- 4. Select a name for your application and set its Type to Foundation. Click Next.
- 5. Select a name for your project folder, and a directory to store your project files in. Click Save.
- 6. In the left pane, you will see the file main.m. Highlight that file. Type your program into the edit window that appears in the rightmost pane.
- 7. In the toolbar, select the middle icon under View. This will reveal the Debug area. That's where you'll see your output.
- 8. Build and run your application by clicking the Run button in the toolbar or selecting Run from the Product menu.
- 9. If you get any compiler errors or the output is not what you expected, make your changes to the program and rerun it.

### Note

Xcode contains a powerful tool known as the static analyzer. It does an analysis of your code and can find program logic errors. You can use it by selecting Analyze from the Product menu or from the Run button in the toolbar.

### Using Terminal

Some people might want to avoid learning Xcode to get started programming with Objective-C. If you are used to the UNIX shell and command-line tools, you might want to edit, compile, and run your programs using the Terminal application. Here we examine how to go about that.

The first step is to start the Terminal application on your Mac. The Terminal application is located in the Applications folder, under Utilities. Figure 2.10 shows its icon.

![](img/9a03a17dbf1900dce936c9665ab15c26_28_0.png)

Figure 2.10 Terminal program icon

Start the Terminal application. You'll see a window that looks like Figure 2.11.

![](img/9a03a17dbf1900dce936c9665ab15c26_28_1.png)

Figure 2.11 Terminal window

You type commands after the $ (or %), depending on how your Terminal application is configured on each line. If you're familiar with using UNIX, you'll find this straightforward.*

First, you need to enter the lines from Program 2.1 into a file. You can begin by creating a directory in which to store your program examples. Then you must run a text editor, as vi or emacs, to enter your program:

```sh
sh-2.05a$ mkdir Progs      Create a directory to store programs
sh-2.05a$ cd Progs           Change to the new directory
sh-2.05a$ vi main.m          Start up a text editor to enter program
```

> Note
> In the previous example and throughout the remainder of this text, commands that you, the user, are entered in boldface.

For Objective-C files, you can choose any name you want; make sure the last two characters are .m. This indicates to the compiler that you have an Objective-C program.

After you've entered your program into a file (and we are not showing the commands to enter and save your text here), you can use the GNU Objective-C compiler, which is called gcc, to compile and link your program. This is the general format of the gcc command:

```bash
gcc -framework Foundation files -o program
```

This option says to use information about the Foundation framework:
- -framework Foundation

Just remember to use this option on your command name., files is the list of files to be compiled. In our example, we have only one such file, and we're calling it main.m. prograde is the name of the file that will execute the program compiles without any errors.

We'll call the program progl; here, then, is the command line to compile your first Objective-C program:

```bash
$ gcc -framework Foundation main.m -o progl      Compile main.m & call it progl$
```

The return of the command prompt without any messages means that no errors are found in the program. Now you can subsequently execute the program by typing the name progl at the command prompt:

```bash
$ progl                                     Execute progl
sh: progl: command not found
$
```

This is the result you'll probably get unless you've used Terminal before. The UNIX shell (which is the application running your program) doesn't know where progl is located (we don't go into all the details of this here), you have two options: One is to precede the name of the program with the characters ./ so that the shell knows to look in the current directory for the program to execute. The other is to add the directory in which your programs are stored (or just simply the current directory) to the shell's PATH variable. Let's take the first approach here:

```bash
$ ./progl Execute progl
2008-06-08 18:48:44.210 progl[7985:10b] Programming is fun!
$
```

You should note that writing and debugging Objective-C programs from the terminal is a valid approach. However, it's not a good long-term strategy. If you want to build Mac OS X or iOS applications, it's just to use the executable file that needs to be "packaged" into an application bundle. It's not easy to do that from the Terminal application, and it's one of Xcode's specialties. Therefore, I suggest you start with.

### Explanation of Your First Program

Now that you are familiar with the steps involved in compiling and running your program, let's take a closer look at this:

```objective-c
// main.m
// Created by Steve Kochan on 2011/06/30
// Copyright 2011 Classroom, Inc. All rights reserved.

#import <Foundation.h>

int main (int argc, const char *argv[]) {
    AutleasePool *pool = [AutleasePool alloc init];
    NSLog(@"Programming is fun!");
    return 0;
}
```

In Objective-C, lowercase and uppercase letters are distinct. You can insert comments into the program in two ways. One is by using two slashes // The compiler ignores any characters that follow up to the end of the line. You can also initiate a comment with the characters /*. This marks the beginning of the comment. These types of comment have to be terminated. End the comment, you use /* All characters included are part of the comment. This form of comment is often used when many lines of code, as in the following:

```objective-c
/*
```

This file implements a class called Fraction, which represents numbers. Methods allow manipulation of fractions, such as addition, subtraction, etc. For more information, consult the document: /usr/docs/classes/fraction.pdf

```objective-c
/*
```

Which style of comment you use is entirely up to you. Just note that you can't nest the * style comments. Get into the habit of inserting comment statements in the program as you write it for three good reasons. First, documenting the program while particular logic is still in your mind is far easier than going back and rethinking the logic after the program has been completed. Second, by inserting comments into the program at an early stage of the game, you can reap the benefits of the comments during the debug phase, when program errors are isolated and debugged. Not only can a comment help you (and others) read through the program, but it can help point out the way to the source of the logic. Finally, I haven't yet discovered a programmer who actually enjoys a program. In fact, after you've finished your program, you will probably not relish the idea of going back to the program to insert comments. Inserting comments while developing the program makes this sometimes tedious task a bit easier to handle.

This next line of Program 2.1 tells the compiler to locate and process a file named Foundation.h:

```objective-c
#import <Foundation.h>
```

This is a system file—that is, not a file that you created. #import serves to import or include the information from that file into the program, exactly as if the contents of file were typed into the program you pointed. You import the file Foundation.h because it has information about other classes and functions that are used later in the program.
