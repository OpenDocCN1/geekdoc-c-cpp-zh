![](bbox=[0.11, 0.11, 0.56, 0.43])

# FIGURE 14-1

5. VS adds a file called PlanetWrox.edmx and two files with a .tt extension and then opens the Entity Designer for you in the main editor window, shown in Figure 14-2. It also installed the EntityFramework package, which resulted in an EF assembly (a .dll file) and XML documentation file in the Bin folder.

This Entity Designer shows you .NET classes that have been generated based on the tables in your database. VS draws a line connecting the two classes, indicating it picked up the relationship that you created between the underlying tables in Chapter 12. If you don’t see the line, or you don’t see Reviews at the bottom of the Genre class or Genre at the bottom of the Reviews class, make sure you set up your database as explained in Chapter 12.

![](bbox=[0.59, 0.47, 0.88, 0.67])

# FIGURE 14-2

6. If you’re using a non-English version of VS you need to pluralize the names of the entity sets and properties yourself. To do this, click the Genre class in the Designer, open its Properties Grid by pressing F4, and change the Entity Set Name from Genre to Genres. Repeat this for the Review class and change its Entity Set Name to Reviews. Finally, click the Review property on the diagram for the Genre class (located under the Navigation Properties header in Figure 14-2), press F2 to rename the item, and enter Reviews as the new name. Because a Review only belongs to a single Genre, you don’t need to pluralize the Genre property of the Review class.

7. Save and close the diagram.

8. Open All.aspx from the Reviews folder, switch it into Design View, and drag a GridView from the Toolbox onto the page. If you don’t have this page, create it now and base it on your custom template.