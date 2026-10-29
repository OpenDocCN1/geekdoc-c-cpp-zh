# Part VI: Advanced Modeling

# FIGURE 24.10

The Asset Tracking interface shows all the checked-out files and the status of each.

![](bbox=[0.084, 0.174, 0.603, 0.474])

# Selecting a working folder

When files are checked out from the asset tracking system, they are copied to a local directory on your current machine where the changes are saved until the file is checked back in. The first time you try to check out a file from the asset tracking system, the system asks you to select a working folder. This folder is a temporary folder where the checked out files are saved while being worked on. You can manually set the working folder by selecting the Server➜Options menu command in the Asset Tracking interface.

You can set which warning dialog boxes appear and which are handled automatically using the Options➜Prompts menu command in the Asset Tracking interface. This command presents a list of all the available prompt dialog boxes and lets you right-click each to have it appear or not appear.

The Asset Tracking dialog box has commands for checking files in and out under the File menu. Each time a file is checked in, a confirmation dialog box appears, as shown in Figure 24.11. In this dialog box, you can enter a comment about the latest changes. The file is then saved to the Vault server with an incremented version number. The ability to save and keep track of different versions of a file is known as “version control” and is one of the key features of an asset management system.

An Undo Checkout command is available in the File menu that throws away the current changes and restores the current Vault file.

# Getting and adding Vault files

After a database is created for a project and you’ve logged in, you can add open files to the Vault server using File➜Add Files menu command. This command adds the current file to the Vault project folder, but the file must be saved to the local working folder before it can be added to the Vault folder. You can select multiple files such as bitmap textures by holding down the Ctrl key while clicking them; you also can add multiple files at the same time using this command.