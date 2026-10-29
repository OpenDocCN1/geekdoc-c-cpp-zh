# Note

To maintain version control of your Max scenes, use the Increment on Save feature instead of increasing the Number of Autobak Files.

+   4. Set the Backup Interval to the amount of time to wait between backups.
+   The Backup Interval should be set to the maximum amount of work that you are willing to redo. (I keep my settings at 15 minutes.) You can also give the Auto Backup file a name.

+   5. Auto Backup saves the files in the directory specified by the Auto Backup path. To view where this path is located, choose Customize ▸ Configure User Paths.

# Maintaining log files

You can also use the Files panel to control log files. Log files keep track of any errors and warnings, general command info, and any debugging information. You can set log files to never be deleted, expire after so many days, or keep a specified file size with the latest information. If your system is having trouble, checking the error log gives you some idea as to what the problem is. Logs are essential if you plan on developing any custom scripts or plug-ins. You can select that the log contain all Errors, Warnings, Info, and Debug statements.

Each entry in the log file includes a date-time stamp and a three-letter designation of the type of message with DBG for debug, INF for info, WRN for warning, and ERR for error messages, followed by the message. The name of the log file is Max.log.

# Importing and Exporting

If you haven't noticed, Max isn't the only game in town. A number of different 3D packages exist, and exchanging files between them is where the importing and exporting menu commands come in. You can find both of these commands in the File menu.

# Importing supported formats

Choose Application Button ▸ Import ▸ Import to open the Import dialog box. This dialog box looks like a typical Windows file dialog box. The real power comes with the various Import Settings dialog boxes that are available for each format. These dialog boxes appear after you select a file to import. The settings in the Import Settings dialog box are different for the various format types.

Max can import several different formats. All acceptable files are automatically displayed in the file dialog box, or you can filter for a specific format using the Files of Type drop-down list at the bottom of the file dialog box. The available import formats include the following:

+   - Autodesk (FBX)
+   - 3D Studio Mesh, Projects, and Shapes (3DS, PRJ, SHP)
+   - Adobe Illustrator (AI)
+   - Collada (DAE)
+   - LandXML/DEM/DDF
+   - AutoCAD and Legacy AutoCAD (DWG, DXF)
+   - Flight Studio OpenFlight (FLT)