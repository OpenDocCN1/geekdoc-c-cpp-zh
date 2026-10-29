# Cross-Ref

More details on using Schematic View are covered in Chapter 25, “Working with the Schematic View.”

When a Max file created in a previous version of Max is opened, a warning dialog box appears that says, “Obsolete data format found—Please resave file.” To eliminate this warning, disable the Display Obsolete File Message option. The warning dialog box also includes an option to Don’t Display Again that enables this option when selected.

When textures are updated, the Reload textures on change option forces the textures to be reloaded when they are altered. This slows your system while Max waits for the textures to reload but offers the latest look immediately.

The Recent Files in File Menu option determines the number of recently opened files that appear in the Application Button Recent Documents menu. The maximum value is 50.

# Backing up files

The Auto Backup feature in Max can save you from the nightmare of losing all your work because of a system crash. With Auto Backup enabled, you can select the number of Autobak files to keep around and how often the files are backed up. The backup files are saved to the directory specified by the Configure Paths dialog box. The default is to save these backups to the 3dsmax\autoback directory. You can also select a name for the backup files.

# Note

Even if you have this feature enabled, you should still save your file often.

This is how it works: If you’ve set the number of backup files to 2, the interval to five minutes, and the backup name to MyBackup, then after five minutes the current file is saved as MyBackup1.max. After another five minutes, another file named MyBackup2.max is saved, and then after another five minutes, the MyBackup1.max file is overwritten with the latest changes.

If you lose your work as a result of a power failure or by having your toddler accidentally pull out the plug, you can recover your work by locating the Autobak file with the latest date and reloading it into Max. This file won’t include all the latest changes—only updates up to the last backup save.

# Tip

I highly recommend that you keep the Auto Backup option enabled. This feature has saved my bacon more than once. Also, if you enter a different autoback name for different projects, then you won’t accidentally overwrite a backed-up project.

# Tutorial: Setting up Auto Backup

Now that I have stressed that setting up Auto Backup is an important step to do, here’s exactly how to set it up.

To set up the Auto Backup feature, follow these steps:

+   1. Open the Preference Settings dialog box by choosing Customize Preferences, and click the Files panel.
+   2. Turn on Auto Backup by selecting the Enable option in the Auto Backup section.
+   3. Set the number of Autobak files to 5.