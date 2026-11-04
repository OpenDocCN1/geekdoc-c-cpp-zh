+   2. If the Toolbox is auto-hiding (it should be after you first install Visual Studio), float the mouse over it until it expands. Click the thumbtack to pin it.
+   3. To display the Output window, open the View menu and select Output. Grab the Output window's title bar and drag it around. Move it over some drop targets to see where it lands. When you're finished, drop it at the bottom of the IDE as shown in Figure 1-7.

# Run the program.

+   1. Press F5 or open the Debug menu and select Start Debugging.
+   2. Try out the form's minimize, maximize, and close buttons and the commands in the form's system menu. Move the form around and resize it. Marvel at the fact that you didn't need to write any code!

# Find the program's executable, copy it to the desktop, and run it there.

+   1. Start File Explorer and navigate to the location that you specified when you created the new program.
+   2. There you should find a folder named after the program. Open that folder and examine the files inside. Notice the .sln file that you can double-click to reopen the solution in Visual Studio. Notice also the bin, obj, and .vs directories.
+   3. Enter the bin directory and move into its Debug subdirectory. It contains several files including the executable, named after the program but with the .exe extension. Right-click the executable and select Copy.
+   4. Right-click the desktop and select Paste to copy the executable to the desktop.
+   5. Double-click the copy of the executable on the desktop.

# Copy the project folder to a new location and make changes to the copy.

+   1. In File Explorer, go to the directory that contains the project folder.
+   2. Right-click the project's folder and select Copy.
+   3. Right-click the desktop and select Paste to copy the project folder.
+   4. Open the copied project folder and double-click the .sln file to open the copied project in Visual Studio. If the form doesn't open in the Form Designer (#4 in Figure 1-7), look in Solution Explorer and double-click the file Form1.cs.
+   5. In the Form Designer, grab the handle on the form's lower-right corner and resize the form to make it tall and skinny.
+   6. Run the modified program. Then go back to the original project (which should still be running in another instance of Visual Studio) and run it. Notice that the two versions display forms of different sizes.

# Compress the project folder to make a backup.

+   1. In Visual Studio, close the project. (Or close Visual Studio.)
+   2. In File Explorer, return to the project's folder and delete the bin, obj, and .vs directories. (Note that you can't delete the bin directory if Visual Studio has the project open.)