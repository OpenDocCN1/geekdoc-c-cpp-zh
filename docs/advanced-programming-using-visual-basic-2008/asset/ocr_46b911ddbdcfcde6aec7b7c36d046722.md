+   - In the IDE's Solution Explorer, rename the solution and the project. The best way to do this is to right-click on the name and choose the *Rename* command from the shortcut menu. To rename the solution, you must display the solution name. Select *Tools / Options / Projects and Solutions / General / Always show solution*.
+   - Rename the forms, if desired. If you rename the startup form, you must open the Project Designer (*Project / ProjectName Properties*) and set the Startup Object.
+   - Open the *Project Properties* dialog and change the assembly name to match your new project name.
+   
+   *Warning:* Do not try to copy a project that is open using the *Save As* command, attempting to place a copy in a new location.

# Refresh the Database in an Update Program

When you write a database update program, you must test all options, including adding records, deleting records, and modifying records. With a little caution, you can delete the modified version of the database and replace it with an unchanged version.

# How Windows Applications Handle the Database File

When you set up a new data source, the wizard asks you whether you want to add the database file to the project folder. To make your projects portable, you should always say Yes. But when you run the application, another copy is made, into the bin\Debug (or bin\Release) folder. Your program actually updates the copy in bin\Debug.

The version of the file that you retrieve for each program run depends on a property of the database file. Select the file in the Solution Explorer and set the property for Copy to Output Directory to Copy if newer. By default, the property is set to Copy always, which means that, for every program run, you get a new, fresh copy of the file and cannot see changes made on the last program run. With the Copy if newer setting, each time you run the application, VS checks the timestamp on the two copies of the database: if they are the same or the file in bin\Debug is newer, no copy is performed. But if the file in bin\Debug is older or no file exists in bin\Debug, then the file from the project folder is copied as the application begins to run.

You can easily return to the original version of the data file by deleting the copy in bin\Debug. In addition to the .mdf file (the main database file), you also must delete the log.ldf file, which holds the index and timestamp information.

You may not be able to see the database files in the Solution Explorer initially. Select Show All Files and click the Refresh button; then expand the bin\Debug folder nodes to see the .mdf and .ldf files. You can delete the files directly in the Solution Explorer by right-clicking and selecting Delete.