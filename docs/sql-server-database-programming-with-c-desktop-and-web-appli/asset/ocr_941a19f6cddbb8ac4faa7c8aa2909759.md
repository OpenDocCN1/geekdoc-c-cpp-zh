# Introduction to Databases

![](bbox=[0.118, 0.075, 0.881, 0.313])

Figure 2.57 The modified image column.

Performing the operations to add all students into the **Student** table in our sample database **CSE_DEPT**

+   1) Open our **SQL Image Project** if it is not opened, and after right clicking on our **SQL Image Project** in the Solution Explorer, and select **Add | New** item from the popup menu.

+   2) In the opened New Item Wizard, select the **Item (Forms)** and select **Form2.cs** into the **Name** box at the bottom. Click on the **Add** button.

+   3) Open the **Data Sources** window and right click on our added Dataset,CSE_DEPTDataSet, and select the **Configuration Data Wizard** to configure it or add the Student table into this Dataset.

+   4) In the Configuration Wizard, select the **Fields** table and the Student table, and check only three columns: **student_id, student_name** and **simage**.

+   5) Your finished **Student** table in the Configuration Wizard is shown in Figure 2.58. Click on the **Finish** button to complete this configuration process.

+   6) Return to our **C# NET** project and focus on our added Form2 window. First expand our Data **CSE_DEPTDataSet** and the **Student** table in the Data Sources window. Click on the drop down over the **Student** table combo box and select the **Details** item, and then drag this place it into the Form2 window.

+   7) Go to the **image** object added to the Form2 window, **simage**, and click on an arrow box located at the upper-right corner to open the **PictureEdit** dialog box, and select **Stretch** from the Size mode box. Then click on any Form2 window to close that PictureEdit dialog box.

+   8) Perform a similar operation as we did in step 6, click on the drop down over the **GridView** table combo box, and then drag this GridView and place it into the Form2 window.

+   9) Go to **File | Save All** to save all of these additions and modifications.

+   10) Now double click on the **Program.cs** file in the Solution Explorer to open it, then go to coding line 19 and replace the code **Application.Run(newForm1())** with **Application.Run(newForm2())** to run our Form2.

+   11) Then click on the **Start** button (green arrow on the tool bar) to run this C# project. As the project runs, the contents of three columns for all students in this **Student** table are displayed in the Details and GridView except the student image **simage**, as shown in Figure 2.59.