# Data Selection Query with Visual C#.NET

![](bbox=[0.118, 0.093, 0.881, 0.396])

FIGURE 5.111 The opened Visual Studio.NET installer.

Linq. We select it by clicking the checkbox in front of it and click the OK button to add this reference to our project.

Next we need to create entity classes using LINQ to SQL tools provided by Visual Studio.NET to set up mapping relationships between each physical data table and the related entity class. We prefer to use the Object Relational Designer Since Visual Studio 2017, the LINQ to SQL is no longer available by default installation of that IDE. Perform the following operations to get and add it into your project:

+   - On the opened project, go to Tools | Get Tools and Features item to open the Visual Studio Installer.
- On the opened installer, select the Individual components on the top, scroll down the component list until you find the item, LINQ to SQL tools (Figure 5.111).
- Check the checkbox in front of item to select it, and click the Modify button on the Database lower-right corner to add it into your project.

You can choose the Visual Studio.NET Installer when downloading process is complete.
One point to note is that you may need to close any opened Visual C# project to complete downloading this and installation process.

# 5.17.2 Create Entity Classes and Connect the Data to the DATABASE

To open the Object Relational Designer, right-click our LINSelect Project from the Solution explorer, select the Add | New Item from the popup menu to open the New Item wizard. Select the item LINQ to SQL Classes by clicking on it, and select CSE_DEPT.dbml into the Name box as the name for this intermediate DBML file, as shown in Figure 5.112. Then click the Add button...
The intermediate DBML file is an optional file when you create the entity classes and this file allows you to control and modify the names of those created entity classes and properties; it agrees