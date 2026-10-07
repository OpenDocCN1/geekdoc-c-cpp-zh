
# Introduction to Databases

![](img/d59a47501d0a20fc0460a49c469c6fb7_77_0.png)

**Figure 2.53** Drag and drop three columns in GridView format table.

- 14) Now go to the Image object added on the Form window, **fimage**, and click on an arrow box located at the upper-right corner to open the **PictureEdit Tasks** dialog, and select **Stretch** from the **Size Mode** box. Then click on any of the Form window to close that PictureEdit dialog box.
- 15) Perform a similar operation as we did in step 12, click on the drop-down arrow of the Faculty table box and select the **GridView**, then then drag this GridView item and place it into the Form window, as shown in Figure 2.53.
- 16) Now go to **File | Save All** to save all of these additions and modifications to this Form window.
- 17) Click on the **Start** button (green arrow on the tool bar) to run this Visual C# project. As the project runs, the contents of three columns for all faculty members in this **Faculty** table are displayed in the Details and GridView except faculty **fimage**, as shown in Figure 2.54.
- 18) To add an image to the **fimage** box for the selected faculty, click on an arrow for that faculty and first click (left-left) on the **faculty** column in the GridView, and then right-click on the **faculty** column. On the popup menu, select the **Load** image to try to load and add an image for the selected faculty member.
- 19) Browse to the latest folder, in case all faculty images are stored in the folder: **Students\Faculty** in the CRS Fpt file. You can copy those images and save them in one of your folder in your machine. Browse to folder and select the associated faculty image, such as **Anderson.jpg** for the faculty member **Black**, clicking on it, and click on the Open button to add it to the **CSE_DEPTDataset**.
- 20) Then click on the **Save Data** button located at the upper-right corner of the tool bar to save this image into the database. Perform similar operations to add all faculty images into our sample database **CSE_DEPT.db**.

Your finished Form window is shown in Figure 2.54. Now you can start stopping the running of the Visual C#.NET project **SQL Image Project** by clicking on the **Close** button.

The relationships between each faculty member, student and related name of image file as shown in Figures 2.55 and 2.56.

# 50 SQL Server Database Programming with C#

![](img/d59a47501d0a20fc0460a49c469c6fb7_78_0.png)

**FIGURE 2.54** The completed form for adding faculty images.

| faculty_id | faculty_name | fimage |
|---|---|---|
| A52990 | Black Anderson | Anderson.jpg |
| A77587 | Debby Angles | Angles.jpg |
| B66750 | Alice Brown | Brown.jpg |
| B78880 | Ying Bai | Bai.jpg |
| B86590 | Davis Bhalla | Davis.jpg |
| H99118 | Jeff Henry | Henry.jpg |
| J33486 | Steve Johnson | Johnson.jpg |
| K69880 | Jenney King | King.jpg |

**FIGURE 2.55** The image files in the faculty table.

| student_id | student_name | simage |
|---|---|---|
| A78835 | Andrew Woods | Woods.jpg |
| A97850 | Ashley Jade | Jade.jpg |
| B92996 | Blue Valley | Valley.jpg |
| H10210 | Holes Smith | Smith.jpg |
| T77896 | Tom Erica | Erica.jpg |

**FIGURE 2.56** The image files in the student table.

Now if you are using the SQL Server Management Studio 18 and the database **CSE DEPT**, select and open the Faculty table with **Edit Top 200 Rows item**, you can find that all **NULL** in the faculty column become to **Binary data**, as shown in Figure 2.57.

In a similar way, you can add students' images into the Student table in our database **CSE DEPT mdf**. All students' images can be found under a folder Students\images\Students at the CRC fip site (Figure 1.2 in Chapter 1). One can copy and store them in a local folder in your computer. The relationships between each student and related name of image file are shown in Figure 2.56.

# Introduction to Databases

![](img/d59a47501d0a20fc0460a49c469c6fb7_79_0.png)

Figure 2.57 The modified image column.

Performing the operations to add all students into the **Student** table in our sample database **CSE_DEPT**

- 1) Open our **SQL Image Project** if it is not opened, and after right clicking on our **SQL Image Project** in the Solution Explorer, and select **Add | New**.
- 2) In the opened New Item, select the **Item (Forms)** and select **Form2.cs** into the **Name** box at the bottom. Click on the **Add**.
- 3) Open the **Data Sources** window and right click on our added Dataset, CSE_DEPTDataSet, and select the **Configuration Wizard** to configure it.
- 4) In the Configuration Wizard, select the **Fields** table and the Student table, and check only columns: **student_id, student_name** and **simage**.
- 5) Your finished **Student** table in the Configuration Wizard is shown in Figure 2.58. Click on the **Finish** button.
- 6) Return to our **C# NET** project and focus on our added Form2 window. First expand our **CSE_DEPTDataSet** and the **Student** table in the Data Sources window. Click on the drop down over the **Student** table and select the **Details** item, and then drag this into the Form2 window.
- 7) Go to the **image** object added to Form2 window, **simage**, and click on an arrow box located at the upper-right corner to open the **PictureEdit** dialog box, and select **Stretch** from the Size mode. Then click on any Form2 window to close that PictureEdit dialog box.
- 8) Perform a similar operation as we did in step 6, click on the drop down over the **GridView** table box, and then drag this GridView and place it into the Form2 window.
- 9) Go to **File | Save All** to save all of these additions and modifications.
- 10) Now double click on the **Program.cs** file in the Solution Explorer to open it, then go to coding line 19 and replace the code **Application.Run(newForm1())** with **Application.Run(newForm2())** to run our Form2.
- 11) Then click on the **Start** button (green arrow on the tool bar) to run this C# project. As the project runs, the contents of three columns for all students in this **Student** table are displayed in the Details and GridView except the student image **simage**, as shown in Figure 2.59.

# SQL Server Database Programming with C#

![](img/d59a47501d0a20fc0460a49c49c6fb7_80_0.png)

FIGURE 2.58 The finished table in the data source configuration.

![](img/d59a47501d0a20fc0460a49c469c6fb7_80_1.png)

FIGURE 2.59 The completed form for adding student images.

- 12) To add an image to the **simage** box for the selected student, click on an arrow for that student and first click (left-click) on the **simage** column in the GridView, then right-click on the **simage** column again. On the popup menu, select the *Load* item to try and add an image for the selected student.
- 13) Browse to the related student image, in our case, all student images are stored in the folder: `Students\images` in the CRC Press site. You can copy those images and save them in one of your local folder in your machine. Browse to that local folder and select the associated student image, select **Erica.jpg** for the student **Tom Erica**, by clicking on it and click on the **Open** button to add to DataSet.
- 14) Then click on the **Save Data** button located at the upper-right corner of the tool bar to save this image into the database. Perform similar operations to add all student images into our sample database **CSE_DEPT.mdf**.

# Introduction to Databases

Your finished Form2 window is shown in Figure 2.59. Now you can stop the running of the Visual C#.NET SQL Image Project by clicking on the **Close** button.

A completed projects, SQL Image Project, can be found from the folder Class DB Projects\Chapter 2 under the Students folder in the CRC fps site (refer to Figure 1.2 in Chapter 1).

# 2.10 A SHORT-CUT: HOW TO USE THE DATABASE WITHOUT BUILDING IT

If users, for some reason or other, do not have time or not to create and build this sample database, CSE_DEPT, with these steps, they can take a short-cut to directly use this database without spending any time or efforts. The precondition is that the following components must be installed:

* Microsoft SQL Server 2019 Express Database
* Microsoft SQL Management Studio 18

Refer to Appendix A on the CRC fps site to get more details in how to install Microsoft SQL Server 2019 Express Database and Microsoft SQL Management Studio. Refer to Appendix E on the CRC fps site to get more details in how to copy, this database file and attach it into the SQL Server 2019 Express Database via the SQL Server Management Studio.

# 2.11 CHAPTER SUMMARY

A detailed discussion and analysis of the structure and components about popular database systems are provided in this chapter. Some key technologies in developing and designing a database are given and discussed in this part. The procedure and components used to develop a relational data-base are analyzed in detail with some real-data tables in our sample database CSE_DEPT. The process in developing and building a sample database is discussed in detail with the following points:

*   Defining Relationships
* Normalizing the Data
* Implementing the Relational Data
