little Scala program into a text file that ends with “.scala” and run it by putting the file name after the scala command on the command-line.

# 2.4 End of Chapter Material

# 2.4.1 Summary of Concepts

+   - The software you use to interact with your computer comprises a tool set. The nature of these tools is extremely important to software developers.
+   - The first half of this book is written with the expectation the reader is using command-line tools. These vary between operating systems.
+   - Linux and Unix based operating systems, including Mac OS X, include a powerful command-line that is often utilized.
+     - There are a number of different commands that you use to give instructions to the computer using the command-line. You will likely commit these to memory over time as you use them. The real power of these commands is that they can be given arguments to make them behave in specific ways or do specific things.
+     - Files are organized in directories. Some of the most important commands you will need to learn are for dealing with directories and navigating the directory structure. The name . always represents the current directory and .. represents the parent directory.
+     - Input and output for commands can be redirected in different ways.
+       * Use > to send the output of a program to a file, deleting anything that is there.
+       * Use >> to send the output of a program to a file, appending to the end of current contents.
+       * Use < to have the contents of a file act as the standard input for a program.
+       * Use | to have the output of one program sent to the input of another. You can chain multiple programs together with this technique called “piping”.
+     - Programs are typically written in plane text with a text editor. The text editor described in this chapter is vi. It is very common on Linux/Unix installs and the capabilities of the command mode make it a good editor for programming.
+   - Windows also incorporates a command prompt that resembles the older DOS interface.
+     - There are a different set of commands that you can use in the Windows command prompt. I/O redirection works like it does in Linux/Unix.
+     - The command-line text editor is called edit. It is not included in 64-bit Windows installs. You can use Notepad or some other GUI text editor. Microsoft Word and other word processing programs are not text editors.
+   - When you install Scala on your computer you get a number of different executable commands.
+     - The scala command can run scripts or applications. If no argument is given it opens up the REPL for you to type in individual statements.