```
public double StakeHeight;
}
public class Carrot : Vegetable
{
    public double Depth;
}
```

To create a class library like this, follow these steps:

+   1. Create a new Class Library project.
+   2. Replace the default code with a listing of your own.
+      You can use the one in this section, if you want.
+   3. Build the class library by pressing Ctrl + Shift + B.
+   4. Right-click on the project and select View Class Diagram.
+      Visual Studio creates a new file called ClassDiagram1.cd. This is your Class Diagram file.
+   5. Save your project.

You can add methods to your new class as well. Click on the Methods of the Flower class and add a Water method by typing Water under name Void under type, and Public under modifier. If you change back to the library view, you'll find that there has been a method added to the code under that class.

![](bbox=[0.03, 0.62, 0.18, 0.78])

To aid in documentation of projects, you can right-click anywhere in the designer pane and select Export This Diagram as an Image, and then save it off as a .PNG file. I find this immensely useful when I am creating documentation for a project. It is a lot more useful than Visio because its integrated with your code, included in Visual Studio, and it's free!

# Data View

Data View is usually used with the Server Explorer and is part of an in-studio representation of SQL Management Studio. You can view and edit data tables in the SQL Server (and other) database management system right inside Visual Studio. An example is shown in Figure 2-5.

There is a remarkable amount of power here, and there just isn't enough space to cover it all. Again, this isn't a database book, so I recommend reading over the MSDN entries for the Data Connections feature of SQL Explorer for more details.