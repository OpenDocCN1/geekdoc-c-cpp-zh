# The form that’s displayed when you run the Invoice Total project

![](bbox=[0.154, 0.112, 0.83, 0.489])

# Description

+   - To *run* a project, click the Start button in the Standard toolbar (the one with the green arrowhead and project name on it), select the Debug→Start Debugging menu command, or press the F5 key. This causes Visual Studio to *build* the project and create an assembly. Then, if there are no build errors, the assembly is run so the project’s form is displayed as shown above.
+   - If syntax errors are detected when a project is built, they’re listed in the Error List window and the project does not run.
+   - To locate the statement that contains the error, you can double-click on the error description in the Error List window. After you’ve corrected all the errors, run the project again to rebuild it and clear the errors.
+   - You can build a project without running it by selecting the Build→Build Solution command.
+   - When you build a project for the first time, all of the components of the project are built. After that, only the components that have changed are rebuilt. To rebuild all components whether or not they’ve changed, use the Build→Rebuild Solution command.