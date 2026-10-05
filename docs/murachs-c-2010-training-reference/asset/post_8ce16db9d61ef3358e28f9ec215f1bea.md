
# The Solution Explorer as a form file is being renamed

![](img/3148667e42d4db35b3d08576aaa1fa01_72_0.png)

# How to rename a file, project, or solution

- You can rename a file, project, or solution by right-clicking on it in the Solution explorer window and selecting the Rename command from the shortcut menu. Or, you can select the file, project, or solution in the Solution Explorer and then press F2. Then, you can enter the new name for the file, project, or solution.
- Do not change or omit the file extension when you rename a file. Remember that using a three-letter prefix to identify the contents of the file (like frm for a form file) makes it easier to tell what each file represents.
- When you change the name of a form file, Visual Studio will also change the Name property for the form and update any references within the existing code for the form, which is exactly what you want.

# How to save a file, project, or solution

- You can use the Save All button in the Standard toolbar or the Save All command in the File menu to save all files and projects in the solution.
- You can use the Save button in the Standard toolbar or the Save command in the File menu to save a file, project, or solution. The files that are saved depend on what's selected in the Solution explorer window. If a single file is selected, just that file is saved. If a project is selected, the entire project and its solution are saved. And if a solution is selected, the entire solution and all its projects are saved.
- If you try to close a solution that contains modified files, a dialog box is displayed asking if you want to save those files.

Figure 2-9 How to name and save the files of a project

# Perspective

If you can design the Invoice Total form that is presented in this chapter, you've taken a critical first step toward learning how to develop Windows Forms applications with Visual Studio 2010. The next step is to add the code that makes the form work the way you want it to, and that's what you'll learn to do in the next chapter.

# Terms

- template
- label
- text box
- button
- primary control
- property
- tab order
- focus
- access key

# Exercise 2-1 Design the Invoice Total form

This exercise will guide you through the process of starting a new project and developing the user interface for the Invoice Total form shown in this chapter.

### Set the default path and start a new project

1. Start Visual Studio. If you want to change the import and export settings to make sure your menus are the same as the ones in this book, use the Tools->Import and Export Settings command described in figure 2-1 to specify the default Visual C# development settings.

2. Use the Tools->Options command to display the Options dialog box as shown in figure 2-1. Then, expand the Projects and Solutions group, select the General category, and change the projects location setting to C:\C#2010.

3. If the Save New Projects When Created box and the Always Show Solution box aren't checked, check them.

4. If you want to start the Start Page from appearing each time you start Visual Studio, click on Startup within the Environment group. Then, select another option from the At Startup drop-down list.

5. If you're interested, take a few minutes to review the other options available in this dialog box. Then, close the dialog box.

6. Start a new project as shown in figure 2-2. The project should be named InvoiceTotal and it should be stored in the C:\C#2010\Chapter02 folder; and the solution should be stored in its own folder.

### Add controls to the new form and set the properties

7. Use the techniques in figure 2-4 to add controls to the form so they have approximately the same sizes and locations as in 2-5. Don't worry about the size of the labels, just their locations.

8. Select groups of controls and use the buttons in the Layout toolbar to size and align the controls. But again, let the labels automatically size themselves. Then, size the form so it looks like the one in figure 2-4.

9. Use the Properties window to set properties for the form and for controls so it looks like the form in figure 2-3. These properties are summarized in figure 2-8.

10. Use the View→Other Windows→Document Outline command to open the window for Document Outline view. Next, use this window to check that you've named all of the controls that have Name properties in figure 2-8. Then, click on the controls in this view to see what happens, and close this window when you're done.

### Test the user interface

11. Press F5 to build and run the project. That should display the form in the center of the screen, and it should look like the one in figure 2-3.

12. Experiment with the form to see what it can do. When you press the Tab key, notice how the form moves from one control to another. When you click a button, notice how it enters and pops back just like any other Windows button. Nothing happens in response to these button clicks, though, because you haven't written the code for them.

Notice that the Calculate button has a dark outline around it to indicate that its function will be executed if you press the Enter key. (If it doesn't have a dark outline, you haven't set the AcceptButton property of the form to the button.)

When you press the Alt key, notice that an underline appears under the s in Subtotal, the first c in Calculate, and the x in Exit to indicate that you can use an access key to work with these controls. (If the underlines don't show, you haven't entered the Text correctly.)

13. If you notice that some of the properties are set incorrectly, click the Close button in the upper right of the form to close the form. Then, make the necessary changes and run the project again. When you're satisfied that the form is working right, close the form to return to the Form Designer.

### Experiment with the properties for the form and its controls

14. In the Form Designer, click on the form so it is selected. Then, if necessary, adjust the Properties window so you can see the description for each property. To do that, drag the boundary of the window up.

15. Click on the Categorized button at the top of the Properties window to display the properties by category. Then, review the properties in the Appearance, Behavior, Layout, and Style categories. Although you won't understand all of the descriptions, you should understand some of them.

16. In the Window Style change, change the settings for MaximizeBox and MinimizeBox to false to see how that changes the form. Then, undo those changes, click twice on the Undo button in the Standard toolbar or press Ctrl+Z twice.

17. Click on the first text box and review the Appearance, Behavior, and Layout properties for that control. Here, repeat this for one of the labels and one of the buttons. Here again, you won't understand all of the descriptions, but you should understand some of them.

18. Select all four of the labels, click on the ▷ symbol before the Font property in the Appearance group, and press the Bold setting to true to see how that changes the form. Then, undo that change.

### Change the name of the form files

19. Use one of the techniques presented in figure 2-9 to change the name of the form file from Form1.cs to frmInvoiceTotal.cs. When you do that, a dialog box is displayed asking whether you want to change all of the references to the form name too. Click on Yes to change that dialog box, and Visual Studio changes all references to Form1 in the C# code that has been generated to frmInvoiceTotal.

20. Note in the Solution Explorer that this also changes the name of the two subordinate files to frmInvoiceTotal.Designer.cs and frmInvoiceTotal.resx.

### Close the project and exit from Visual Studio

21. Use the File→Close Solution command to close the project. If you've made changes to the project since the last time you tested it, a dialog box is displayed asking whether you want to save the changes that you made. If you want to save those changes, click Yes.

22. Use the File→Exit command to exit from Visual Studio.
