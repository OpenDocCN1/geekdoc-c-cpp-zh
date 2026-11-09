+   10. *Click* the **Dock in Parent Container** link in the Smart Tag of the ListView control to dock the **ListView** control in its parent container (form), (Fig.VB-7.31).

![](bbox=[0.178, 0.176, 0.502, 0.375])

![](bbox=[0.521, 0.176, 0.846, 0.375])

After designing the user interface for the form, the next step in developing a LINQ to SQL application is to include a LINQ to SQL class in the application. In the succeeding steps, you learn to include a LINQ to SQL class in the application.

+   11. *Right-click* the project name, **LINQtoSQL**, in **Solution Explorer** and select **Add→New Item** from the context menu that appears, (Fig.VB-7.32).  
+      The **Add New Item** dialog box opens (Fig.VB-7.33).  
+   12. *Select* **LINQ to SQL Classes** in the middle pane of the **Add New Item** dialog box (Fig.VB-7.33).  
+   13. *Enter* **MyClass.dbml** as the name of the class in the **Name** text box (Fig.VB-7.33).  
+   14. *Click* the **Add** button to add the LINQ to SQL class to the current project, (Fig.VB-7.33).

![](bbox=[0.193, 0.523, 0.422, 0.707])

![](bbox=[0.451, 0.523, 0.831, 0.707])

The LINQ to SQL class, **MyClass.dbml**, is added to the **LINQtoSQL** project and opens in Object Relational Designer (Fig.VB-7.34). In the succeeding steps, you need to create data classes from where you will take data for your application by dragging items from **Server Explorer** onto **Object Relational Designer**. You can notice in Fig.VB-7.34 that Object Relational Designer is divided into two panes. The left pane, called the entities pane, is the design surface that shows the entity classes, associations, and inheritance hierarchies. The right pane, called the methods pane, is the design surface that shows the methods of the **DataContext** class (in our case, the **MyClassDataContext** class) that are mapped to the stored procedures and functions in a database.

+   15. *Click* the **Server Explorer** link in the left pane of Object Relational Designer to open **Server Explorer**, as shown in Fig. VB-7.34.