# # How to finish your design

When you’re working on a project, you may want to change the names of some of the files from their defaults. Then, you’ll want to save the files with their new names.

# ## How to rename the files of a project

You may have noticed throughout this chapter that I didn’t change the default name of the form (Form1.cs) that was added to the Invoice Total project when the project was created. In practice, though, you usually change the name of this form so it’s more descriptive. For example, figure 2-9 shows how to use the Solution Explorer to change the name of the form file from Form1.cs to frmInvoiceTotal.cs. When you do that, Visual Studio will also change the File Name property for the form from Form1 to frmInvoiceTotal, and it will ask you if you want to modify any references to the form.

You may also want to change the name of the project or solution. For example, if you accepted the default project name when you started the project (WindowsApplication1.proj), you may want to change it to something more meaningful. Or, you may want to change the name of the solution so it’s different from the project name. If so, you can use the technique presented in this figure to do that too.

# ## How to save the files of a project

Figure 2-9 also describes how to save the files of a project. Because Visual Studio saves any changes you make to the files in a project when you build the project, you won’t usually need to save them explicitly. However, it’s easy to do if you need to.

When using the Save or Save All command, two factors determine which files are saved: what’s selected in the Solution Explorer and the command you use to perform the save operation. If, for example, a single file is selected, you can use the Save command to save just that file, and you can use the Save All command to save the file along with the project and solution that contain the file. In contrast, if a project is selected in the Solution Explorer, the Save command causes the entire project to be saved, and the Save All command causes the entire solution to be saved.

If you haven’t saved all of your recent changes when you close a project, Visual Studio will ask whether you want to save them. As a result, you don’t need to worry that your changes will be lost.