+   - Getting familiar with the most frequently used services of Visual Studio

+   - Deploying add-ins

> If you want to get more information on add-in development, check out the book Professional Visual Studio Extensibility by Keyvan Nayeri (Indianapolis: Wiley, 2008).

If you feel you even more than what is available with Visual Studio add-ins, and you want to create more complex extensions, Visual Studio packages will be your best friends.

# VISUAL STUDIO PACKAGES IN A NUTSHE

The most powerful way to develop Visual Studio extensions is integrating Visual Studio packages (VSPackages) into the IDE. These packages are not limited to using the automation model, or only to a few core services, but can access the whole infrastructure of Visual Studio just like the packages created by the development team at Microsoft.

This book does not get into great detail about VPackage development, but instead provides a general overview. To examine the most important concepts in the context, let's build a simple functional package just to scratch the surface.

# Creating a Package with a Simple Menu Command

A VPackage is a class library containing the types responsible for the package infrastructure and functionality. In order for Visual Studio to recognize the compiled class library as a package, encapsulated types should have specific metadata information, and some additional steps are required after compilation. So, even if you could start a package from an empty class library, it is much easier to use the VPackage wizard with the VS SDK.

# Using the VPackage Wizard

Start a new project with the File New New project function. The IDE displays the New File dialog to select the desired project type. You can find the Visual Studio Integration Package project type under the Other Project Types category in the Extensibility folder, as shown in Figure 6-24.