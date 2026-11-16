Figure 3.3 shows what the project looks like in the ECLIPSE PROJECT EXPLORER view once it's been created. Here, we can see that the project creation wizard has furnished us with everything we need to get started with development, including the following:

+   1. Underneath the JAVA RESOURCES node, you can see that a folder called src has been created to store our Java source code files.

+   2. The project also contains references to all of the libraries needed to build Java-based web applications. This includes the basic Java SE libraries, Java EE libraries, and SAP HCP-specific libraries.

+   3. A WEBContent folder mirrors the structure of the WAR file that will be used to deploy our web folder. As you can see, this includes the aforementioned prebuilt web.xml deployment descriptor.

![](bbox=[0.14, 0.39, 0.43, 0.64])

Figure 3.3 Basic Structure of a Dynamic Web Project in Eclipse

The last step in the project setup process involves the creation of a Java package to store our Java source files. To create a new package, simply right-click on the src folder and select the New • PACKAGE menu option, as shown in Figure 3.4. Then, in the New JAVA PACKAGE dialog box, specify the package name using the familiar Java package naming convention based on reverse Internet domain names (see Figure 3.5).