# Using the System.DataNamespace 433

![](bbox=[0.228, 0.142, 0.584, 0.566])

2-15:
Looks like a class model, walks like a database.

Book III
Chapter 2

Access Data

Notice something missing? The Asset_Parts table is gone; it's been abstracted into the model for you the table was there to link the Assets and Tables in a many-to-many relationship. Slick, isn't it?

# Writing code for the entity model

After you have interesting addition to your coding environment and the database is meshed nicely into the C# object model, you can code with the objects provided in this entity model. To start, follow these steps:

+   1. Go back to the window designer and double-click the window to go to Code View.
2. In the window, load event handler, type Part part = new Part().
3. In the next line, type part and check out the IntelliSense. It contains all columns in the Parts table as properties to the class.

What you now have is a context to work against. No complex Linq queries—they're all done under the covers. In inline SQL. No stored procedures. You can do it all with with scoped object.