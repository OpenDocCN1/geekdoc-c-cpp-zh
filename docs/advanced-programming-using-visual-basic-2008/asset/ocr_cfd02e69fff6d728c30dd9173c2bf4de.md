The project’s .exe file is the executable, which is used to run the program; the .pdb file holds debugging information. If you are distributing your application, you only need to distribute the .exe file, not the .pdb file. The ProjectName.vshost.exe file is a small application that runs the project in the environment.

# Project Resources

The Resources folder holds resources that you add to your project. Figure 1.6 shows a graphic file stored in the Resources folder; you can also add sound files and text strings to the resources.

![](bbox=[0.22, 0.42, 0.52, 0.68])

> Figure 1.6
> The Resources folder holds the project resources, such as graphic and sound files, and text strings.

Visual Studio provides several ways to add resources to the folder and to access those resources. You can add resources in the Project Designer, discussed later in this chapter. You also can add resources from the Properties window, such as when you set the Image property of a PictureBox control. At design time, you can assign properties of controls to resources that are in the Resources folder, and you can retrieve resources at run time using the My.Resources object, which also is discussed later in this chapter.

Each form in your project also has a resource file, which has a .resx extension. For example, Form1.vb has a Form1.resx file, which you can see in the Solution Explorer when you click on the Show All Files button and expand the form’s node.

The .resx file is mostly text in XML format, which you can open and view in the IDE. The .resx file holds pointers to the files in your Resources folder and supplies the resources to the form at compile time. Any graphic elements that you add to the form, such as a PictureBox’s Image property or a form’s Icon property, also are stored in the .resx file in text that represents the binary graphic file.

If you rename your form file in the Solution Explorer, the .resx file is automatically renamed to match. At times you may find extra .resx files in the project’s folder; you can safely delete any extra .resx files if their names do not match any forms in the project.

# Image Files in Visual Studio 2008

Microsoft is including many graphic files with Visual Studio 2008. The graphics are those used in Windows so that you can make your applications use the standard images. The default location for