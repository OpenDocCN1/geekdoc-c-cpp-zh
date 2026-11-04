You can create your own outlining, too. Preceding a section that you want to outline, put `#region` on a new line. After that section, put `#endregion`. This newly defined section — regardless of whether it's at an existing outline point — will get a new outline mark.

If there is a comment added after a `region` statement, it will show in the collapsed outline — as you can see in Figure 2-12.

# ## Exploring the auxiliary windows

A number of windows affect text input and output in order to solve certain problems. As a group, they don't really have a name, so I call them auxiliary windows. I cover four of them here.

![](bbox=[0.1, 0.41, 0.25, 0.51])

+   - **The Output window:** I use the Output window regularly for two things:
+     - *Build logging.* Every time you build, the Output window tracks all of the linking and compiling that goes on under the sheets and shows any errors that might come up.
+   
+       By default, the Output window shows when you build. You can set it to not show the Visual Studio Options dialog box, after choosing General>Projects and Solutions.
+   
+       Errors listed in the Output window can be used to navigate the code. The buttons in the Output box assist with getting around the code based on the messages in the window.
+     - *Debug statements:* The second use of the Output window is Standard Out (for all you C++ people). If you use a `Debug.Write` statement in your code, the Output window is where it will go. Additionally, if you use `Console.Write`, but are running a Windows Forms application, for instance, the text will go to the Output window.
+   - **The Immediate window:** This window does exactly what one would expect it to do — it does something immediately. In debug mode, you can use the Immediate window to send commands to the program as it is running, to change the state, or evaluate operations. Try this to see what I mean:
+     1. Open a Windows Forms project.
+   
+        The one in the sample code for this chapter on this book's companion Web site is fine — you just need a default project template.
+     2. Put a breakpoint on `form_load`. Do this by clicking in the grey bar running down the side of Code View.
+   
+        A red dot should appear.

![](bbox=[0.1, 0.76, 0.25, 0.87])