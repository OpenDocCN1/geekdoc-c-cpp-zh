# CREATING A **FRAMEWORK**

In addition to using system and third-party frameworks, it can be useful to create your own. One simple benefit is that you can place code that is shared between a Mac OS version and an iOS version of your application in a single, common location. Both can link against the same framework and benefit from improvements and bug fixes from the same source.

To familiarize you with this process, you’ll create a simple framework in a separate project and learn how to build it for release so it’s ready to use in other projects. In Chapter 16, you’ll learn how to combine projects into a single workspace, allowing Xcode to recognize it as a dependency and build and include it in TestApp automatically.

# CREATE THE PROJECT

To create a new project, choose File > New > New Project from the main menu. Choose the Framework & Library group under the Mac OS X section. Select Cocoa Framework from the list and click Next.

The project options sheet (**Figure 15.10**) will appear. In the Product Name field, enter **TestAppSharedFramework** so you can distinguish it from the TestApp project. It’s also a good idea to make sure the Company Identifier value is the same as the one you gave for the TestApp project. You can deselect the Include Unit Tests check box for simplicity. Click Next.

Select the “Create local git repository for this project” check box and select the same folder that contains the TestApp project folder (the TestApp folder’s parent). Make certain you don’t save it in the TestApp project folder, but one level above. Click Create to create the project. You should have a shiny new project window, as seen in **Figure 15.11**. Now you’re ready to add some code.