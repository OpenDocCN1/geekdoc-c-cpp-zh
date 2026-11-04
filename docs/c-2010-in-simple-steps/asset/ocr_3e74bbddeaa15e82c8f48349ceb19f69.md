Now that you have learned about some important properties, methods, and events of the ToolStripItem class, let's create a Windows Forms application named ToolStripDemo, where we can use some of these properties, methods, and events. Perform the following steps to create the ToolStripDemo application:

+   1. Click Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010 to open the Visual Studio 2010 integrated development environment (IDE).
+   2. Select File→New→Project from the menu bar to open the New Project dialog box.
+   3. Select Visual C#→Windows from the Installed Templates pane of the New Project dialog box.
+   4. Select Windows Forms Application from the right-hand side of the Installed Templates pane.
+   5. Enter ToolStripDemo as the name of the application in the Name text box.
+   6. Enter the path of the folder where you want to save the application in the Location combo box. In our case, we have selected the default location, which is C:\Users\temp\Documents\Visual Studio 2010\Projects.
+   7. Click the OK button in the New Project dialog box. The ToolStripDemo application is created.
+   8. Select the Form1 form that appears in the designer and press the F4 key to view its properties in the Properties window. Set the Text and Size properties of the Form1 form to ToolStripDemo and 479, 300 respectively.
+   9. Drag a Label control from Toolbox and drop it on to the Form1 form in the designer and set its Text and Location properties to This is a demonstration of the ToolStrip control and 97, 127 respectively.
+   10. Drag a ToolStrip control from the Menus & Toolbars tab of Toolbox and drop it on the Form1 form in the designer. The Form1 form now appears, as shown in Fig.C6-6.1:

![](bbox=[0.2, 0.58, 0.78, 0.78])

Fig.C6-6.1

Note that the ToolStrip control, toolStrip1, appears at the top of the Form1 form as well as in the component tray, which is displayed as a rectangular strip at the bottom of the designer of the Form1 form. This is because the Dock property of the toolStrip1 control is set to Top, by default. You can change the Dock property to Left, Right, Fill, Bottom, or None. Now, you need to add tool strip items to the toolStrip1 control. You can add tool strip items either at design time or at run time. Let's perform the following steps to add the tool strip items to the toolStrip1 control at design time:

11 Select the toolStrip1 control in the designer and press the F4 key to open the Properties window.