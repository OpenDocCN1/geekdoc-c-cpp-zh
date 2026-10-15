settings are contained in the directory with it, which enables the different versions to run with unique settings. Before we are done going through the project properties, we will add an app.config file to this project.

For now however, you have a new project and an initial Windows Form, Form1, available in the Solution Explorer. In this case, the Form1.vb file is the primary file associated with the default Windows form Form1. You'll be customizing this form shortly, but before looking at that, it would be useful to look at some of the settings available by opening your project properties. An easy way to do this is to right-click on the My Project heading shown in Figure 1-4.

# Project Properties

Visual Studio uses a vertically tabbed display for editing your project settings. The project properties display shown in Figure 1-5 provides access to the newly created ProVB_VS2010 project settings. The project properties window gives you access to several different aspects of your project. Some, such as Signing, Security, and Publish, are covered in later chapters. For now, just note that this display makes it easier to carry out several tasks that once required engineers to work outside the Visual Studio environment.

![](bbox=[0.14, 0.34, 0.8, 0.73])

FIGURE 1-5

You can customize your assembly name from this screen, as well as reset the type of application and object to be referenced when starting your application. However, resetting the type of your application is not recommended. If you start with the wrong application type, it is better to create a new application, due to all the embedded settings in the application template. In the next section you will look at a button for changing your assembly information, as well as the capability to define a root namespace for your application classes. Namespaces are covered in detail in Chapter 4.

You can also associate a given default icon with your form (refer to Figure 1-5), and select a screen other than the default Form1 as the startup screen.

Near the middle of the dialog are two buttons. Assembly Information is covered in the next section. The other button, labeled View Windows Settings refers to User Access Control settings, which enable you to