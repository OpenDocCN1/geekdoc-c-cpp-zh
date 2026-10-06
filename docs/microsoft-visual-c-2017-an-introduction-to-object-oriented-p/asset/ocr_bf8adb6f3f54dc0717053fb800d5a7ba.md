# CHAPTER 3 Using GUI Objects and the Visual Studio IDE

For example, you might double-click a Label1 named label1 by mistake and generate a method named label1_Click(). You can leave the automatically created method empty so that no actions result, in a professional program you typically not include empty methods. Such empty methods that never execute are known as orphaned methods. You should not delete an orphaned method, behind the scenes, other code might have been created that refers to the method; if so, the program will not compile. Instead of deleting the method code, you should click on the unwanted method so it appears in the Properties window, click the Events button, which looks like a lightning bolt. Select the event you want to eliminate, and delete the name of the method (see Figure 3-15). This eliminates all the references to the method, and your program can run again successfully.

118

![](bbox=[0.137, 0.327, 0.584, 0.533])

**Figure 3-15** Deleting an event from the Properties window

# Failing to Close a Form Before Attempting to Reexecute a Program

Often you will execute a GUI application and notice something you want to correct in the program. For example, you might want to reward the Text on Label1, or reposition a Button on the Form. In your haste to make the improvement, you might forget to close the application that is still running. If you make a change to the program and then try to rerun it, you will get an error message that indicates that changes are not allowed while the program is running. The solution is simply to close the previous execution of the application and then try again.

# Using Visual Studio Help

When working with a class that is new to you, such as Button or Form, no book can answer your questions. The ultimate authority on C classes is the Visual Studio Help documentation. You should use this tool as you continue to learn about C# in particular and the Visual Studio products in general. The Help documentation for Visual Studio is the MSDN Library, which you can install locally on your own computer. It is also available at http://msdn.microsoft.com.

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN-022-200-202