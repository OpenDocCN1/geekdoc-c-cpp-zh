As with most other projects in VS 2010, you can create different build configurations. Use the Configuration combo box to select the build configuration for which you want to alter properties. In Figure 34-4, notice that you are modifying the properties for the currently active build configuration: Debug. The button labeled Configuration Manager enables you to add, remove, and edit the build configurations for this project.

The Output File Name setting can be used to modify where the resulting Windows Installer package (.msi) file is created. You can modify the filename and path directly, or you can click the Browse button.

# Package Files

The next setting, Package Files, enables you to specify how the files that make up the installation are packaged. The possible options are:

+   - As loose uncompressed files-When you build the project, the files that are to be included as part of the installation are copied to the same directory as the resulting Windows Installer package (.msi) file. As mentioned earlier, this directory can be set using the Output file name setting.
+   - In a setup file-When the project is built, the files that are to be included as part of the installation are packaged in the resulting Windows Installer package file. When you use this method, you have only one file to distribute. This is the default setting.
+   - In cabinet file(s)-With this option, when the project is built, the files that are to be included as part of the installation are packaged into a number of cabinet files.

# Prerequisites

Prerequisites are standard components that may be needed to install or run the application but are not a part of it. There are several of these, as shown in Figure 34-5, which shows the dialog that is displayed when the Prerequisites button is clicked.

The .NET Framework is checked by default, and so is the Windows Installer. You should only uncheck these if you are sure that all the machines on which your application will be installed already have the correct versions of these prerequisites installed. As mentioned earlier in this chapter, Visual Studio 2010 allows targeting of the .NET Framework version you would like to use, so the targeted version of the framework needs to be coordinated with the prerequisites.

![](bbox=[0.47, 0.38, 0.81, 0.6])

If the box for any of these prerequisites is checked, then the resulting installation package will automatically check for the presence of that prerequisite, installing it if required. If you are installing from a CD or network share, then it is common for the packages that install these prerequisites to be placed in the same location as your installation package. The default settings assume that this is true and install the prerequisites from that location.

However, you can specify a different location for packages that install prerequisites. You can select the “Download prerequisites from the following location:” option at the bottom of the dialog and then specify the URL at which the packages are located. Alternately, you can select “Download prerequisites from the component vendor’s web site,” and then the Installation URL on the previous dialog will be used (refer to Figure 34-5).