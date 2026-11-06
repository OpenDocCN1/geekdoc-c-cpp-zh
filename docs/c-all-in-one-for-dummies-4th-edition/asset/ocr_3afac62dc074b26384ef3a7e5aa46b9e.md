Use the Browse for Folder dialog box to locate the folder you want to use. Notice that the wizard completes the entry in the Project Filename field.

+   5. **(Optional) Type a project filename in the Project Filename field.**
+   
+   Code::Blocks fills in this field for you automatically based on the Project Title field entry, and there isn’t a good reason to change it in most cases; however, in special circumstances, you may choose to do so. For example, if you have a project with multiple elements, you may want the project file to match the name of an overall project rather than the name of a particular entity within the project.

+   6. **Click Next.**
+   
+   You see the compiler settings shown in Figure 3-3. Most of the projects in this book use the default compiler settings, which include the GNU GCC Compiler shown in the figure. However, if you look at the Compiler drop-down list, you see that Code::Blocks supports a number of compilers and you can add more to it. The other settings control the creation and location of a Debug version of the application (the version you use for finding problems in your code) and a Release version (the version that you send to a customer).

![](bbox=[0.248, 0.464, 0.656, 0.738])

**FIGURE 3-3:** Tell Code::Blocks where to place the Debug and Release versions of your application.

+   7. **(Optional) Change any required compiler settings.**
+   
+   There generally isn’t any good reason to change the compiler settings unless your project has a specific need, such as placing the output and object files in the same folder.