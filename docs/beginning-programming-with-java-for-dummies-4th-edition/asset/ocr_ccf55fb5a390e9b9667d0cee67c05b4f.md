# *Running the code*

To have Eclipse run the code, do the same thing you do with any other Java program. Select the project you want to run (project 13-02 in this example). Then choose **Run > Run As > Java Application**.

When you run the program in Listing 13-2, no text appears in Eclipse’s Console view. This total lack of any noticeable output gives some people the willies. The truth is, a program like the one in Listing 13-2 does all its work behind the scenes. The program has no statements that read from the keyboard and has no statements that print to the screen. So, if you have a very loud hard drive, you may hear a little chirping sound when you choose **Run > Run As > Java Application**, but you won’t type any program input, and you won’t see any program output.

The program sends all its output to a file on your hard drive. So what do you do to see the file’s contents?

# *Viewing the output file*

To see the output of the program in Listing 13-2, follow these steps:

+   1. In the Project Explorer, select the `13-02` project branch.
+   2. In the main menu, choose **File > Refresh**.
+   3. In the Project Explorer, expand the `13-02` project branch.
+      A new file named `cookedData.txt` appears in the Package Explorer tree (in the 13-02 project).
+   4. Double-click the `cookedData.txt` branch in the Package Explorer tree.

The contents of `cookedData.txt` appear in an Eclipse editor. (See Figure 13-5.)

![](bbox=[0.23, 0.713, 0.56, 0.839])