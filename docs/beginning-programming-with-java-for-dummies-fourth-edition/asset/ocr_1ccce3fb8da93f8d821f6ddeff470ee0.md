diskWriter, you can use any names you want. All you have to do is to use the names consistently within each of your Java programs.

**A call to the close method ends the connection between your program and the file.**

In many of this book's examples, you sever the connection between your program and the computer keyboard by calling `keyboard.close()`. The same is true when you call the `close` method for a disk file's scanner or a disk file's `PrintStream` instance. Calling the `close` method reminds Java to finish all pending read or write operations and to break the program's connection to the disk file, the keyboard, or to whatever else holds data for the program.

This book's examples are pretty simple. If you omit a `close` method call in one of these examples, you might get a warning message from Eclipse, but the world doesn't end. (That is, your program still runs correctly.) However, in a serious, make-it-or-break-it application, the proper placement of `close` calls is important. These `close` calls ensure the proper completion of the program's input and output actions and help free up disk resources for use by other running programs.

# Running the sample program

Testing the code in Listing 13-2 is a three-step process. Here's an outline of the three steps:

+   1. Create the `rawData.txt` file.
+   2. Run the code in Listing 13-2.
+   3. View the contents of the `cookedData.txt` file.

The next few sections cover each step in detail.

# Creating an input file

You can use any plain old text editor to create an input file for the code in Listing 13-2. In this section, I show you how to use Eclipse's built-in editor.

To create an input file:

+   1. Select a project in Eclipse's Package Explorer.
+   
+   In this example, select the 13-02 project (the project containing the code from Listing 13-2).
+   
+   In the Package Explorer, select a branch whose label is the name of a project. (Select the 13-02 branch to run the code in Listing 13-2.) Don't select an item within a project. (For example, don't select the src branch or the (default package) branch.)

![](bbox=[0.12, 0.92, 0.22, 0.99])