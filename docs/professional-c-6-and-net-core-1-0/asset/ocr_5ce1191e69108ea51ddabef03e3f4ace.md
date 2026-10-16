![](bbox=[0.106, 0.06, 0.894, 0.259])

# Figure 18.6

Now there are more things that need to be done with VSIX projects. The project contains the file source .extension.vsixmanifest. This file is the description of the add-in and needs to be configured. When you open this file from Visual Studio, a special designer for configuring Metadata, Install Targets, Assets, and Dependencies also opens.
Metadata configuration is shown in Figure 18.7. With these settings you define the description, license, release notes, and images that should show up. When you configure Install Targets, you define your Visual Studio edition and what add-in should be available. With Visual Studio 2015, you can define the add-in to be available only with the Enterprise edition or also with the Professional and Community editions. You can also define that the add-in should be available with the Visual Studio shell. The shell of Visual Studio is used with several projects from Microsoft or third parties.

![](bbox=[0.106, 0.555, 0.894, 0.903])

# Figure 18.7