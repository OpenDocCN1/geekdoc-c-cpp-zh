![](bbox=[0.027, 0.102, 0.552, 0.249])

There are a few benefits to this, and they are fairly important.

+   - **Division of labor:** First, it separates the C# server code from the ASP.NET and HTML template code. Although it doesn't do a perfect job, it's a lot better than scripting languages like Active Server Pages and PHP that have everything merged together. It just makes things easier to keep track of.
+   - **Speed and security:** Using this pattern, Microsoft compiles the C# code into a DLL, just like the class libraries Book II delves into. This makes the application much faster and protects the application somewhat from criminals.
+   - **Legacy-based:** This pattern mimics Windows Forms development, going back to Visual Basic 3. It is easy for people to pick up if they already have experience. I know that history isn't always the best to mimic, but it can't hurt.

# Scripting the experience

Using the code-behind isn't the only way to skin this digital cat, though. If you want to take a trip back to the nineties, you can code your C# right into an ASPX file, with your controls in your HTML.

However, if you can't tell, I am not in favor of this method. It compiles at runtime, rather than at design time, so it is slower. The code is all junked together, making it hard to find anything.

Nonetheless, sometimes you have to do this. I once deployed a Web project to a hosting company that wouldn't let me upload a .DLL file. I had to rewrite the whole app into inline script so that it would run. Knowing how to do this is important.

Let me give you an example. Let's start with the project you were editing earlier. From there, follow these steps:

+   1. Right-click on the project and select **Add New Item**.
+   2. In the dialog box that comes up, select **Web Form**, as shown in **Figure 2-7**.
+   
+      See the red box (added) at the bottom of Figure 2-7? By default, it is checked.