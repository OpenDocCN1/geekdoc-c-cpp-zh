# 426 Using the System.DataNamespace

Depending on what edition of SQL Server you have installed, you may see extra steps. You may be asked by Visual Studio to upgrade the data-base file, which is totally fine. If you're in a large-scale enterprise environment, check with your database administrator as the best way to connect to your database system.

![](bbox=[0.229, 0.23, 0.715, 0.566])

**Figure 2-6:** The Change Source dialog box.

If you do use a database file, Visual Studio will copy pertinent files to your project. If you're working through this book in an isolated project, that's fine. If you're on a development effort with others, check to make sure it's appropriate to your life cycle methodology.

+   7. Click the Next button to save the connection string to the application configuration file.

+   8. Accept the defaults by clicking Next.

You see the Choose Database Objects and Settings screen. You can choose the tables, views, or stored procedures that you want to use.

+   9. Under Tables, select Product and ProductCategory (under the Production heading, as shown in Figure 2-7), and click Finish.

You're done! If you look at the designer, you can see that an Entity Data Model was added to your project with the two tables on the design surface, as shown in Figure 2-8.