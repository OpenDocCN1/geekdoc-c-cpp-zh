hidden files and folders. The My Project folder holds several files for project configuration, including AssemblyInfo.vb. You will learn to view and set configuration options in the Project Designer, which is discussed in the "The Project Designer" section later in this chapter.

In Figure 1.4, you can see the expanded References collection, the bin and obj folders, and the form files for Form1.vb. You can expand each of the nodes to see more details. Note that the solution name does not display by default. To show the solution name, as in Figure 1.4, select Tools / Options / Projects and Solutions and check Always show solution. You will want to always show solutions so that you can edit solution names.

# References

In the References folder, you can see a list of System libraries (DLLs), such as System, System.Deployment, System.Drawing, and System.Windows.Forms. These are the references included by default for a new Windows application. You can add a reference by right-clicking on the References folder and selecting Add Reference from the context menu. You also can add references in the Project Designer, which is discussed a little later. You may need to add a reference if you want to refer to objects in another assembly or components written in a different language.

# The Bin and Obj Folders

Notice the organization of the bin and obj folders:

+   bin
+     Debug
+     Release
+   obj
+     Debug
+     Release

When you compile and run a project using the debugger, you are running the program stored in the bin/Debug folder. The debug versions of the compiled project are not optimized for release. If you compile a program for release, the compiled versions are placed in the Release folders. Notice the files in the bin/Debug folder in Figure 1.5, which shows the Solution Explorer after compiling a project.

![](bbox=[0.18, 0.78, 0.48, 0.99])

# Figure 1.5

After compiling a project and clicking the Refresh button, the bin/Debug folder holds the files needed to run the program in the debugger.