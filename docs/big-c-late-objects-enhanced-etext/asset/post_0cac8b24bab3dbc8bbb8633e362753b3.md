
```
cout << "Hello, World!" << endl;
}
return 0;
```

We will examine this program in the next section.

No matter which programming environment you use, you begin your activity by typing the program statements into an editor window.

Create a new file and call it hello.cpp, using the steps that are appropriate for your environment. (If your environment requires that you supply a project name in addition to the file name, use the name hello for the project.) Enter the program instructions exactly as they are given above. Alternatively, locate an electronic copy of the program in the source files for this book and paste it into your editor. (You can download the full set of files for this book from its companion site at wiley.com/go/bc10.3.)

An editor is a program for entering and modifying text, such as a C++ program.

As you write this program, pay careful attention to the various symbols, and keep in mind that C++ is case sensitive. You must enter upper- and lowercase letters exactly as they appear in the program listing. You cannot type MAIN or Endl. If you are not careful, you will run into problems—see Common Error 1.2.

C++ is case sensitive. You must be careful about distinguishing between upper- and lowercase letters.

## Step 3 Compile and run the program.

The compiler translates C++ programs into machine code.

The process for building and running a C++ program depends greatly on your programming environment. In some integrated development environments, you simply push a button. In other environments, you may have to type commands. When you run the test program, the message
Hello, World!
will appear somewhere on the screen (see Figures 5 and 6).

![](img/d61019b035dd82beb581604273c0ee6b_39_0.png)

Figure 5 Running the hello Program in an Integrated Development Environment

![](img/d61019b035dd82beb581604273c0ee6b_40_0.png)

### Figure 6 Compiling and Running the hello Program in a Console Window

```
~$ cd cs1/bookcode/ch01
~/cs1/bookcode/ch01$ g++ -o hello hello.cpp
~/cs1/bookcode/ch01$ ./hello
Hello, World!
~/cs1/bookcode/ch01$
```

> The linker combines machine code with library code into an executable program.

It is useful to know what goes on behind the scenes when your program gets built. First, the compiler translates the C++ source code (that is, the statements that you wrote) into machine instructions. The machine code contains only the translation of the code that you wrote. That is not enough to actually run the program. To display a string on a window, quite a bit of low-level activity is necessary. The implementors of your C++ development environment provided a library that includes the definition of cout and its functionality. A library is a collection of code that has been programmed and translated by someone else, ready for you to use in your program. (More complicated programs are built from more than one machine code file and more than one library.) A program called the linker takes your machine code and the necessary parts from the C++ library and builds an executable file. (Figure 7 gives an overview of these steps.) The executable file is usually called hello.exe or hello, depending on your computer system. You can run the executable program even after you exit the C++ development environment.

## Step 4 Organize your work.

As a programmer, you write programs, try them out, and improve them. You store your programs in files. Files have names, and the rules for legal names differ from one system to another. Some systems allow spaces in file names; others don't. Some distinguish between upper- and lowercase letters; others don't. Most C++ compilers require that C++ files end in an extension .cpp, .cxx, .cc, or .C; for example, demo.cpp.

![](img/d61019b035dd82beb581604273c0ee6b_40_1.png)

### Figure 7 From Source Code to Executable Program

Files are stored in folders or directories. A folder can contain files as well as other folders, which themselves can contain more files and folders (see Figure 8). This hierarchy can be quite large, and you need not be concerned with all of its branches.

However, you should create folders for organizing your work. It is a good idea to make a separate folder for your programming class. Inside that folder, make a separate folder for each assignment.

Some programming environments place your programs into a default location if you don't specify a folder yourself. In that case, you need to find out where those files are located.

Develop a strategy for keeping backup copies of your work before disaster strikes.

Be sure that you understand where your files are located in the folder hierarchy. This information is essential when you submit files for grading, and for making backup copies.

You will spend many hours creating and improving C++ programs. It is easy to delete a file by accident, and occasionally files are lost because of a computer malfunction. To avoid the frustration of recreating lost files, get in the habit of making backup copies of your work on a memory stick or on another computer.

![](img/d61019b035dd82beb581604273c0ee6b_41_0.png)

### Figure 8 A Folder Hierarchy

## Programming Tip 1.1

### Backup Copies

![](img/d61019b035dd82beb581604273c0ee6b_41_1.png)

![](img/d61019b035dd82beb581604273c0ee6b_41_2.png)

Backing up files on a memory stick is an easy and convenient storage method for many people. Another increasingly popular form of backup is Internet file storage. Here are a few pointers to keep in mind.

© Tatiana Popova/iStockphoto.

- **Back up often.** Backing up a file takes only a few seconds, and you will hate yourself if you have to spend many hours recreating work that you could have saved easily. I recommend that you back up your work once every thirty minutes.
- **Rotate backups.** Use more than one directory for backups, and rotate them. That is, first back up to the first directory. Then back up to the second directory. Then use the third, and then go back to the first. That way you always have three recent backups. If your recent changes made matters worse, you can then go back to the older version.
- **Pay attention to the backup direction.** Backing up involves copying files from one place to another. It is important that you do this right—that is, copy from your work location to the backup location. If you do it the wrong way, you will overwrite a newer file with an older version.
- **Check your backups once in a while.** Double-check that your backups are where you think they are. There is nothing more frustrating than to find out that the backups are not there when you need them.
- **Relax, then restore.** When you lose a file and need to restore it from backup, you are likely to be in an unhappy, nervous state. Take a deep breath and think through the recovery process before you start. It is not uncommon for an agitated computer user to wipe out the last backup when trying to restore a damaged file.

## 1.5 Analyzing Your First Program

![](img/d61019b035dd82beb581604273c0ee6b_42_0.png)

In this section, we will analyze the first C++ program in detail. Here again is the source code:

```
sec05/hello.cpp
```cpp
1 #include <iostream>
2
3 using namespace std;
4
5 int main()
6 {
7     cout << "Hello, World!" << endl;
8     return 0;
9 }
```

The first line,

`#include <iostream>`

tells the compiler to include a service for “stream input/output”. You will learn in Chapter 8 what a stream is. For now, you should simply remember to add this line into all programs that perform input or output.

The next line,

`using namespace std;`

tells the compiler to use the “standard namespace”. Namespaces are a mechanism for avoiding naming conflicts in large programs. You need not be concerned about namespaces. For the programs that you will be writing in this book, you will always use the standard namespace. Simply add using namespace std; at the top of every program that you write, just below the #include directives.

The construction

```
int main()
{
    return 0;
}
```

defines a function called main that “returns” an “integer” (that is, a whole number without a fractional part, called int in C++) with value 0. This value indicates that the program finished successfully. A function is a collection of programming instructions that carry out a particular task. Every C++ program must have a main function. Most C++ programs contain other functions besides main, but it will take us until Chapter 5 to discuss functions and return values.

For now, it is a good idea to consider all these parts as the “plumbing” that is necessary to write a simple program. Simply place the code that you want to execute inside the braces of the main function. (The basic structure of a C++ program is shown in Syntax 1.1.)

Every C++ program contains a function called main.
