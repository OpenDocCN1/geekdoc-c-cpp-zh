# # Accessing and Installing Perl

If you are adept at DOS, you can now navigate to the MyPerlPrograms directory and type the name of your file. Figure 2.14 illustrates how you type the name of the file. The *.pl extension invokes the Perl interpreter. The file executes as shown in Figure 2.14.

![](bbox=[0.188, 0.193, 0.59, 0.275])

# ## Figure 2.14
The Hello World Perl program executes at the command prompt.

Alternatively, open Windows and navigate to your MyPerlPrograms directory. You’ll see your file represented with an icon for the Perl interpreter. Figure 2.15 illustrates the situation. Double-click the name of the file.

![](bbox=[0.188, 0.384, 0.59, 0.496])

# ## Figure 2.15
Click on the Perl program in your Windows directory.

A command prompt window opens as the file executes. See Figure 2.16. Press Enter to exit the program.

![](bbox=[0.188, 0.585, 0.59, 0.657])

# ## Figure 2.16
A command prompt window opens, and the Perl program executes.

If your files flash and disappear when you click on them in Windows Explorer, it is usually for one of two reasons. One is that they contain code problems. This problem must be dealt with in due course. On the other hand, the problem might be simply that they contain no code that causes the execution of the file to pause long enough to allow you to see it. To remedy this situation, open the Perl file with Notepad (or your editor) and type the following line right at the end of the file:

$AnyChar = <STDIN>;

You can also type only the following:

<>