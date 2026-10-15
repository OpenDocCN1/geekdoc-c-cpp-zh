# Switching between the Windows

Shortcuts are special keys (or a combination of keys) that perform a specific task or raise a particular event when pressed together. In an IDE, such combinations are mainly used to switch between windows. The following is the list of some of the major shortcuts used to switch between the Windows Forms designer and the Code Editor:

+   - Using the F7 key to switch from one window to another
+   - Using the TAB key in case two windows are opened
+   - Double-clicking the Windows Forms designer for switching from the design view to the code view
+   - Right-clicking the code view and selecting the View Designer option to switch from the code view to the design view
+   - Right-clicking the design view and selecting the View Code option to switch from the design view to the code view
+   - Select View → Code to switch from the design view to the code view
+   - Select View → Designer to switch from the code view to the design view

# Specifying the .NET Framework Version for Projects

Prior to the release of Visual Studio 2008, each Visual Studio release supported only a particular version of the .NET Framework. For example, Visual Studio 2003 supported .NET Framework 1.1, and Visual Studio 2005 supported .NET Framework 2.0. However, Visual Studio 2008 and 2010 are designed to support the multi-targeting feature, that is Visual Studio 2008 supports .NET Frameworks 2.0, 3.0, and 3.5; while Visual Studio 2010 supports .NET Frameworks 2.0, 3.0, 3.5, and 4. Now, when you either open an existing project or create a new one using Visual Studio 2010, you can select one of the available versions of .NET Framework. The IDE automatically updates the compilers and features to match with the selected .NET Framework. Note that when you open a project created in an earlier version of .NET Framework, Visual Studio 2010 shows Visual Studio Conversion Wizard, which upgrades a project created in the lower version of Visual Studio to Visual Studio 2010.

Figure 1.80 shows the Visual Studio Conversion Wizard:

![](bbox=[0.235, 0.535, 0.715, 0.805])

# Customizing the IDE

The Visual Studio 2010 IDE is highly customizable, i.e. you can modify its look and feel, assignment of shortcuts, and other features according to your requirements. Let’s consider an example where you need to change the font and color of the Code Editor window. To do this, select Tools → Options to open the Options dialog box. Then, select the Fonts and Colors page from the Environment folder on the left side of the Options dialog box.