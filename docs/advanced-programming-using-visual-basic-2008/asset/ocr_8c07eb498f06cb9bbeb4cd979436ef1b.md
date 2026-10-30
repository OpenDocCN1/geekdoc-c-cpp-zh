# Deploying Web Projects

Visual Studio offers two methods for transferring files to a Web server. You can use the Copy Web Site tool or the Publish Web Site utility. Note that the Publish Web Site utility is not available in Visual Web Developer Express Edition.

# Using the Copy Web Site Tool

Using Visual Studio 2008, you can create local Web Sites, IIS Web Sites, FTP sites, or remote sites. The Copy Web Site tool allows you to copy files between any of the Web Site types created with Visual Studio using an FTP-style utility.

To run the Copy Web Site tool, right-click the project name in the Solution Explorer or open the Website menu, then select Copy Web Site. The Copy Web Site tool opens in the VS IDE main document window with the Source Web Site list populated with the files from the open Web site. Select the remote site from the Connections list or click Connect to browse for the site.

The Source Web site is the one that is currently open in the IDE; the remote Web site is the one to which you want to copy the files. Even though you use the designations for the source and remote sites, it is possible to transfer files in either direction. In other words, you can copy a file from the remote site into the IDE site.

![](bbox=[0.12, 0.6, 0.9, 0.9])

An excellent feature of the tool is the ability to synchronize the files between the sites. The synchronize file status may be unchanged, changed, new, or deleted. The tool compares the time stamps on the files at each site to determine the status. The synchronization feature does not allow merging. If two