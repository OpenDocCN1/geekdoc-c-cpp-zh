# SQL Server Database Programming with C#

![](bbox=[0.211, 0.085, 0.786, 0.416])

**FIGURE 2.40** The finished tables and columns dialog box.

To do this cascading, scroll down along this Foreign Key Relationships dialog and expand the item **Table Designer**, when you can find the **INSERT And UPDATE Specifications** item. Expand this item and two sub items are displayed, which are:

+   * **Delete Rule**
* **Update Rule**

The default value for both items is **No Action**. Click on the **No Action** box for the **Delete Rule** item and click on the drop-arrow, and select the **Cascade** item from the list. Perform the same operation for the **Update Rule** item. Your finished Foreign Key Relationships dialog should match one that is shown in Figure 2.41.

In this way, we established the cascaded relationship between the Primary key in the parent table and the Foreign keys in the child table. Later on when you update or delete any Primary key from a parent table, the related foreign keys in the child tables will also be updated or deleted without any additional operations. It is convenient!

Click the **Close** button to close this dialog.

Go to the **File | Save** menu to open the **Save** dialog and click the **Yes** button to save this relationship. When you can select **Yes** or **No** to the **Save Change Script** dialog if it appears.

Now right-click on the **Keys** folder under the **Login** table from the Object Explorer window, and we select the **Refresh** item from the popup menu to refresh this **Keys** folder. Immediately you can find a new foreign key **FK_Login_Faculty** appears under this **Keys**. This is our new created foreign key that sets the relationship between **Login** and **Faculty** tables. You can also confirm and find this new created foreign key by right clicking on the **Keys** folder that is under the **Faculty** table.

# 2.9.4.2 Create Relationship between the Login and the Student Tables

In a way, you can create a foreign key for the **Login** table and set up a one-to-many relationship between the **Student** and the **Login** tables.