Another option to hold the command windows in Visual Studio is to select **Debug, Start Without Debugging** instead of **Debug, Start Debugging** to execute your program. Notice in Figure 1-19 that **Start Without Debugging** is the option immediately below the **Start Debugging** option. If you select **Debug, Start Without Debugging**, it is not necessary to add the additional `Console.Read()` or `ReadKey()` statements. When you use the **Start Without Debugging** option for execution, the user is prompted “Press any key to continue,” as was illustrated earlier in Figure 1-14. This is the preferred method for executing your program.

> Several other shortcuts are available to run your program. Notice as you look at the menu option under **Debug** that Ctrl+F5 is listed as a shortcut for **Start Without Debugging**; F5 is the shortcut for **Start Debugging**. In addition, if you have the **Debug** Toolbars icons on your screen, an open right arrow represents **Start Without Debugging**.

Visual Studio is a highly sophisticated integrated development environment. Appendix A, “Visual Studio Configuration,” includes additional information regarding customizing the development environment and using the debugger for development. Reviewing that material now would be wise.

# # Debugging an Application

It is inevitable that your programs will not always work properly immediately. Several types of errors can occur and cause you frustration. The major categories of errors—syntax and runtime—are discussed in the next sections.

# ## Syntax Errors

When you type source code statements into the editor, you are apt to make typing errors by misspelling a name or forgetting to end a statement with a semicolon. These types of errors are categorized as **syntax errors** and are caught by the compiler. When you compile, the compiler checks the segment of code to see if you have violated any of the rules of the language. If it cannot recognize a statement, it issues an error message, which is sometimes cryptic, but should help you fix the problem. Error messages in Visual Studio are more descriptive than those issued at the command line. But, be aware that a single typing error can create several error messages. Figure 1–20 shows a segment of code, in which a single error causes the compiler to generate three error messages.