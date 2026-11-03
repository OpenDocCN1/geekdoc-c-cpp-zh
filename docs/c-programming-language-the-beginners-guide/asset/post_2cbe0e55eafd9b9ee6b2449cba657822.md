
Point your favorite browser—Chrome, Firefox, Internet Explorer—to that website. On that page, look for the download link. Remember, the page you see below may look different, as web pages do change from time to time.

![](img/7d7500a0ed1507e3351945dfe5a0440d_16_0.png)

Click on the download link. Choose to download the binary release. On the next page, click the link that represents your computer operating system: Windows, Linux, or Mac OS X. For Windows, look for the setup.exe file that includes the MinGW compiler. For example, on the screen below, it says “codeblocks-16.01mingw-setup.exe.” The numbers may change, but that is the link you need.

![](img/7d7500a0ed1507e3351945dfe5a0440d_17_0.png)

For Linux, choose your 32-bit or 64-bit distro. Select a version of Code Blocks that is not testing or debuginfo. Try to match your specific Linux distro by choosing a link to download.

![](img/7d7500a0ed1507e3351945dfe5a0440d_17_1.png)

For the Mac, only one option is shown. Click the link to the right of your choice. We recommend that you use sourceforge.net as the download link. The download starts immediately. Wait until it is complete.

The next step is to find the downloaded file and install Code Blocks. Open the folder containing that file, which is usually the Downloads folder. You might also be able to access that folder from the web browser.

In Windows, double-click the file to open it and begin installation. Work through the installation wizard. Don't worry about any of the options. They are all okay. Eventually, Code Blocks will be installed with a shortcut icon on the desktop. Click the Yes button to start Code Blocks if you like, although it is not necessary to do so right away.

On the Mac and Linux, you need to unpack the archive you downloaded. Double-click the icon in a folder window to unpack the archive. On the Mac, you will end up with a Code Blocks app file, which is secretly a folder. We recommend moving that icon to the Applications folder.

With Linux, double-click to open the archive. At that point, you will have to run the install program depending on how your Linux distro deals with whatever is in the archive. For example, if it is an RPM file, open it to begin package installation. After Code Blocks is installed, you need to get it configured. That topic is covered in another chapter.

## Running Code Blocks

The main window will look like the illustration below:

![](img/7d7500a0ed1507e3351945dfe5a0440d_19_0.png)

This is known as the workspace. To the left, you will see the management panel. This lists the projects that you are working on in Code Blocks. The center is where you will find the editor where you will write the code. At the bottom, you will see a host of tabs. These can display messages or other useful information.

You should take a moment now to configure a few Code Blocks settings that will help you use the IDE in this book. First, choose Settings > Editor. Ensure that there is a check-mark by the option “Show line numbers.” All the other options shown below should be set, which is the default.

![](img/7d7500a0ed1507e3351945dfe5a0440d_20_0.png)

Click the Choose button in the font area to set the font. It is recommended that you use a monospaced font for clarity. Set your editor to a 12-point font so that it shows better on your screen. Click OK to close the general settings window.

Second, adjust the build messages text size. Choose Settings > Environment. Next, click the View icon. Set the message logs font size value to 10 or 12, which is better to see. Once you're done, click OK. Congratulations. Code Blocks is now configured for use together with this book.

You can quit Code Blocks now if you want. If you quit, you may be notified that the perspective has changed. Go ahead and save the perspective, and click on the little box so that you are not bothered with the message again.

Creating programs, or "Programming," usually involves typing the program's source code—instructions—using a programming language, and then compiling and linking the source code together to create the program. The created program usually comes in the form of an .exe file if it is for the Windows operating system, or a .sh file if it is a UNIX-based operating system like Linux or Mac.

You then test run the program to see if the program does what it's intended to do. In other words, run it to see if it is working. In the next chapter, we will show you a demonstration of how this process works in Code Blocks. We will talk about how to create and execute a sample computer program written in the C programming language. In addition, we will also teach you how to root out and fix bugs in your program using the IDE.

Once you've finished installing Code Blocks in your PC, start it up. You'll be presented with the Code Blocks start page. If by chance you're working on a computer that has Code Blocks already installed, and has been used to create programs previously, click on View > Start page on the Code Blocks menu to see the start page.

Majority of the work done on the Code Blocks IDE are project-oriented. Code Blocks C language projects can be a small and simple program, or a huge and complicated online computer game. Typically, Code Blocks projects are created by clicking the Create New Project link on the start page. Do note that this particular step is not required whenever you are viewing and working on C language project files that are taken from a different source other than your own computer.

But if you need to make a new C language project in the Code Blocks IDE, particularly the console programs/applications that we will be using in this book, then select the Console Application option when starting a brand new project.

The next step after writing the source code is to compile and link. In Code Blocks, that step is combined into a single action called Build. To build your project, click the Build icon here:

![](img/7d7500a0ed1507e3351945dfe5a0440d_23_0.png)

The action takes place at the bottom of the screen in the Build log and then Build messages tab. If there are errors in your source code, Code Blocks will display a small red box right beside the line number where the error resides. Click the Build log tab to review the specific messages related to the error.

The error messages will also indicate which line the error resides. If you spot an error in your code, rectify them and then click the Build button again. Once there are no more errors, save the file and re-build the project to make sure everything is okay.

Now, on the Macintosh, you may see a warning about option -s. That’s a linker error and you can ignore it. Click the Run button to witness the program’s brilliance. In Windows, the program runs in a command prompt window. On the Mac and Linux, a terminal window appears. In that window, you may also see any startup scripts you’ve written. Ignore that part of the output. Otherwise, what you see is the program’s output.

Close the output window and return to Code Blocks. In Windows, press the Enter key. If the terminal window does not close in UNIX, just type “Exit” and then press the Enter key. It is recommended that you do this. Otherwise, the terminal windows will stack up. You’re now ready to create your first project. If you shut down Code Blocks, it will ask you whether or not you want to save the perspective. Go ahead and click Yes.

## Chapter 2: Starting Your First C Project

The normal human language has two major parts: syntax and speech. Likewise, the C programming language also has its own syntax and speech. If a person who has no background in computer programming looks at a computer source code, it is likely that they won't be able to make heads or tails out of it. However, once they learn the syntax and the figures of speech of the programming language, it will all begin to make sense.

In this book, we will introduce you to syntax and figures of speech of the C programming language. We will teach you how it is structured, what the main function actually does, and also familiarize yourself with its various functions, keywords, values, variables, and operators.

In the Code Blocks IDE, go ahead and click the "New" button, and then click "Empty file." At this point, you're now going to type a C programming language code in the editor window pane of the Code Blocks IDE. Don't be afraid. You're going to type only one line.

Go ahead and type the word "main," followed by a pair of parentheses and a space, and then lastly, followed by a pair of curly braces or brackets. Once you finish typing that in, press Enter on the keyboard. Your Code Blocks editor should now look like this:

```
1 main() {}
2
```

Now, save the source code file by clicking the Save button. If you need to, choose the specific folder where you want to save
