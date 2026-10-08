# Class.cs
</ProjectItem>
<!-- ... -->
</ProjectItems>

# Wizards

Wizards are great tools to customize templates. If you have ever created a Visual Studio Add-In, Shared Add-In, C++ ATL project, or many other types of projects where a wizard helps to create an application, you definitely know the efficiency of this approach.

This is not so sole privilege of the Visual Studio development team at Microsoft to create wizards! This extensibility point is open for every Visual Studio developer. In discussions, you will learn how easy it is to use a wizard to create a custom template.

Wizards are .NET classes implementing the IWizard interface that can be found in the Microsoft.VisualStudio.TemplateWizard namespace in the Microsoft.VisualStudio.TemplateWizard assembly. If you implement IWizard, you can count on the following features:

+   - Collect information through your UI and use information to create a code skeleton.

+   - Extend the replacement dictionary (placeholder/replacement associations) dynamically.

+   - Declare each file that is part of the original template as to whether it should be added to the target project.

+   - Access (and even change) the project or the item from the template after Visual Studio has finished generating them.

+   - Run custom actions before items are opened in their corresponding editors.

# Comment Sample Selector

To demonstrate the features available through the IWizard interface, let's take a look at a simple example implementing one-page wizard that allows the user to select a heading comment from a list. This list shows you to put the selected comment into the header of the Program.cs file in a console application.

Start the wizard by creating a C# class project, and name it SimpleCommentWizard. Delete the Class1.cs file, you do not need it.

The user uses a WPF dialog as its user interface, so add the following assembly references to the project: PresentationCore, PresentationFramework, and WindowsBase. To access the IWizard interface, you must add references for the EnvDTE and Microsoft.VisualStudio.TemplateWizard assemblies. 

Because the wizard should be in the Global Assembly Cache (GAC) so that Visual Studio can find and load it, you must sign it with a key to ensure it has a strong name. Go to the project properties, and on the Signing tab, click the "Sign the assembly" checkbox and select the <...> from the "Choose a strong name file" combo box. Specify a key filename in the dialog