![](bbox=[0.145, 0.108, 0.229, 0.178])

The Toolbox displays only controls that are appropriate to the file in focus.

So, if you’re running a Windows Form in the designer, you won’t see a database table available to drop. Trust me; if you expect to see a certain control, and it isn’t there, the Toolbox probably isn’t messed up. If there isn’t a file open, the Toolbox is empty. That’s by design.

![](bbox=[0.253, 0.263, 0.876, 0.551])

**Figure 2-8:**  
The Toolbox, with tools.

I can’t tell you how many times I have been expecting to see something in the Toolbox only to find it blank. Then I spend ten minutes tracking down the problem, only to realize that the problem is mine — I didn’t have a file open. I once actually called Microsoft because I couldn’t find a maskedtextbox for my Web Forms project.

There is no maskedtextbox for Web Forms projects.

So keep it in mind that the Toolbox is context-sensitive. It works only when it has a file to work on.

There is one other interesting property of the Toolbox: It can be used to store text clippings, which can be useful for demonstrations and presentations. It is also handy for storing often-used pieces of code (Book I Chapter 1), but snippets (covered in Chapter 3) are even better. To do so, follow these steps:

+   1. **Open a code file.**
+   
+      Anything will do, `.cs` file, `.xaml` file, whatever.