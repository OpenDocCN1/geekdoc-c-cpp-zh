but also to arrange to encrypt those settings, although this behavior is outside the scope of what you can do from Visual Studio.

# Other Project Property Tabs

In addition to the tabs that have been examined in detail, there are other tabs which are more specific. In most cases these tabs are used only in specific situations that do not apply to all projects.

# Signing

This tab is typically used in conjunction with deployment. If you are interested in creating a commercial application that needs to be installed on client systems, you’ll want to sign your application. There are several advantages to signing your application, including the capability to publish it via ClickOnce deployment. Therefore, it is possible to sign an application with a developer key if you want to deploy an application internally.

# My Extensions

The My Extensions tab enables you to create and leverage extensions to Visual Basic’s My namespace. By default, Visual Studio 2010 ships with extensions to provide My namespace shortcuts for key WPF and Web applications.

# Security

This tab enables you to define the security requirements of your application. You’ll need these as part of the ClickOnce publishing process, which is covered as part of deployment in Chapter 34.

# Publish

This tab is used to configure and initiate the publishing of an application. From this tab you can update the published version of the application and determine where to publish it. This tab is also covered in more detail in Chapter 34.

# Code Analysis

This tab is only available for Visual Studio 2010 Premium or Ultimate. The tab enables the developer to turn on and configure the static code analysis settings. These settings are used after compilation to perform automated checks against your code. Because these checks can take significant time, especially for a large project, they must be manually turned on.

# PROJECT PROVB_VS2010

The Form Designer opens by default when a new project is created. If you have closed it, then you can easily reopen it by right-clicking Form1.vb in the Solution Explorer and selecting View Designer from the pop-up menu. From this window, you can also bring up the Code view for this form. However, Figure 1-13 illustrates the default view you see when your project template completes. On the screen is the design surface upon which you can drag controls from the Toolbox to build your user interface and update properties associated with your form.

The Properties pane, shown in more detail in Figure 1-14, is by default placed in the lower-right corner of the Visual Studio window. Like many of the other windows in the IDE, if you close it, it can be accessed through the View menu. Alternatively, you can use the F4 key to reopen this window. The Properties pane is used to set the properties of the currently selected control, or for the Form as a whole.