# Chapter 4: Customizing the Max Interface and Setting Preferences

System Paths dialog box is used to specify where the system looks to load files that Max uses such as fonts, scripts, and plug-ins.

# Configuring user paths

The Configure User Paths dialog box, shown in Figure 4.17, holds the path definitions to all the various resource folders. The dialog box includes three panels: File I/O, External Files, and XRefs.

The main panel in the Configure User Paths dialog box is the File I/O panel. The Project Folder is listed at the top of the dialog box and can be changed in this dialog box or with the Application Button➔Manage➔Set Project Folder menu. This panel includes entries for Animations, Archives, Auto Backup, Bitmap Proxies, Downloads, Export, Expressions, Images, Import, Materials, Max Start, Photometric, Previews, Render Assets, Render Output, Render Presets, Scenes, Sounds, and Video Post. If you select any of these entries, you can click the Modify button to change its path. All paths are set by default to folders contained within the Project Folder, but you can change them to whatever you want. The Make Relative and Make Absolute buttons cause the selected entry to be displayed as a relative path based on the Project Folder or an absolute path.

![](bbox=[0.025, 0.433, 0.474, 0.686])

The Configure User Paths dialog box specifies where to look for various resources.

# Tip

Personally, I like to keep all my content in a separate directory from where the application is installed. That way, new installs or upgrades don’t risk overwriting my files. To do this, simply change the Project Folder to a location separate from the 3ds Max installation directory.

Under the External Files and XRefs panels, you can add and delete paths that specify where Max looks to find specific files. All paths specified in both these panels are searched in the order they are listed when you’re looking for resources such as plug-ins, but file dialog boxes open only to the first path. Use the Move Up and Move Down buttons to realign path entries.

# Caution

Using the Customize➔Revert to Startup UI Layout command does not reset path configuration changes.