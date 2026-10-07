
# Introduction to Databases 43

![](img/d59a47501d0a20fc0460a49c469c6fb7_71_0.png)

FIGURE 2.44 The finished tables and columns dialog.

## 2.9.4.4 Create Relationship between the Student and the StudentCourse Tables

The relationship between the **Student** and the **StudentCourse** tables is one-to-many, and the **student_id** in the **Student** table is a Primary key and the **student_id** in the **StudentCourse** table is a Foreign key.
Right-click on the **Keys** folder under the **dbo.StudentCourse** table from the Object Explorer and select the **Update Foreign Key** from the popup menu.

On the opened **Foreign Keys Relationships** dialog, change the name of this new relationship to **FK_Student_Course_Student** in the **Name** box select the **Identity** item on the right hand side.
In the opened **Tables and Columns** dialog, select the **Student** table from the **Primary key table** combobox and select the **student_id** from the box that is just under the **Primary key table** combobox. Then select the **student_id** from the box that is just under the **Foreign key table** combobox. The finished **Tables and Columns** dialog should match one that is shown in Figure 2.44.

Click on the **OK** button to close this dialog and setup the cascade relationship for **Delete Rule** and **Update Rule** items, and then click the **Close** button to close the **Foreign Key Relationships** dialog. Go to the **File | Save Student** item and click **Yes** for the **Message** box to save this relationship.

Now right-click on the **Keys** folder under the **dbo.StudentCourse** table, and select the **Refresh** item. Then you can find your created key **FK_Student_Course_Student**.

## 2.9.4.5 Create Relationship between the Course and the StudentCourse Tables

The relationship between the **Course** and the **StudentCourse** tables is one-to-many, the **course_id** in the **Course** table is a Primary key and the **course_id** in the **StudentCourse** table is a Foreign key.
Right-click on the **Keys** folder under the **dbo.StudentCourse** table from the Object explorer and select the **New Foreign Key** from the popup menu.

On the opened **Foreign Keys Relationships** dialog, change the name of this new relationship to **FK_Student_Course_Course** in the **Name** box select the **Identity** item on the right hand side.
In the opened **Tables and Columns** dialog, select the **Course** table from the **Primary key table** combobox and select the **course_id** from the box that is just under the **Primary key table** combobox. Then select the **course_id** from the box that is just under the **Foreign key table** combobox. Your finished **Tables and Columns** dialog should match one that is shown in Figure 2.45.

# SQL Server Database Programming with C#

![](img/d59a47501d0a20fc0460a49c469c6fb7_72_0.png)

FIGURE 2.45 The finished tables and columns dialog.

Click the OK to close this dialog and not forget to establish a cascade relationship for the Delete Rule and the Update Rule items, and then click the Close to close the Foreign Key Relationships dialog box. Then go to the File | Save StudentCourse menu item and click Yes for the Message Box to save this relationship.

Now right-click on the Keys folder for the dbo.StudentCourse table, and select the Refresh item. Then you can find our created relationship FK_StudentCourse_Course.

At this point, we complete the relationships among our five data tables. You can close the SQL Server Management Studio 18 now.

A completed Microsoft SQL Server 2019 sample database CSE_DEPT.mdf can be found from the CRC Press ftp site, from fellow Sample Database that is located at the Students footer at that site (refer to Figure 1.2 in Chapter 1). The completed relationships among these tables are found in Figure 2.46.

## 2.9.5 Store Items to the SQL Server 2019 Express Database

When building Faculty and Student tables in sections 2.9.2 and 2.9.3, we need to store faculty and student into the SQL Server 2019 Express database. Due to the new property of SQL Server 2019 database, a project can be stored directly into the database as an object.

With the help of Express developed by Windows UI, we can directly insert a project into SQL Server via Visual Studio without any coding. Follow the CRC Press ftp site to finish downloading and installing the Windows UI component in your computer.

Now Visual Studio 2022 and click File | New Project at the bottom of the Visual Studio. Go to the right-hand side and scroll down the scroll bar to find your desired template, (.NET Framework) with C#, as shown in Figure 2.47. Then click on it to select it and click on the Next to continue.

# Introduction to Databases 45

![](img/d59a47501d0a20fc0460a49c469c6fb7_73_0.png)

FIGURE 2.46 Relationships among tables.

![](img/d59a47501d0a20fc0460a49c469c6fb7_73_1.png)

FIGURE 2.47 The create new project wizard.

# SQL Server Database Programming with C# 46

Perform the following operations to create our new SQL project:

- Enter SQL Project into the Project name and Solution name box, as shown in Figure 2.48. Select a desired local folder on your machine to save this project and click on the Create button to create this C# project.
- The created project wizard is shown in Figure 2.49. Click on the Add Data Source link in the Data Sources located at the lower-left (if this window is not shown, go up to View | Other | Data Sources to open it), to connect to our SQL Server 2019 Express database CSE_DEPT.
- Keep the default Database selection on the next wizard and click on the Next buttons to continue to our database connection page.
- Click on Next Connection to set up a new database object.
- On the chosen Data Source wizard, select Microsoft SQL Server item from Data Source list, then Next.
- The next wizard, Add Connection, is shown in Figure 2.50. Enter the full name of your database server, DESKTOP-JPURF\SQL2019EXPRESS, into the Server name box.
- Click on the dropdown arrow on Select or enter database name, and select your sample database CSE_DEPT from the list. Your finished Add Connection wizard should match one that is shown in Figure 2.50.
- Click the Test Connection button at the lower-left corner to test this connection. A successful connection message should be displayed if this connection is fine. Close the message box and click on the OK button to continue.
- On the next wizard, you can check Show connection string to review this connection string, and we may need this connection string later. Click on the Next button to continue.
- Click on the Next button again on the next wizard to save our connection string.
- Now all data objects or components, including five tables in our sample database, CSE_DEPT, are displayed, as shown in Figure 2.51.

# Configure your project

![](img/d59a47501d0a20fc0460a49c469c6fb7_74_0.png)

# Introduction to Databases 47

![](img/d59a47501d0a20fc0460a49c469c6fb7_75_0.png)

FIGURE 2.49 The new added SQL project.

![](img/d59a47501d0a20fc0460a49c469c6fb7_75_1.png)

FIGURE 2.50 The opened add connection wizard.

# SQL Server Database Programming with C# 48

![](img/d59a47501d0a20fc0460a49c469c6fb7_76_0.png)

**2.51** The connected your dataset CSE_DEPTDataSet.

- Expand the **Tables** and the **Faculty** folder to check our **Faculty** table, and select three columns, **faculty_id**, **faculty_name** and **fimage**, by checking them one by one, as shown in Figure 2.51. Then click on the **Finish** button to complete this database connection and data setup process.
- Return to your Visual Studio window, expand our Dataset and the Faculty table, **CSE_DEPTDataSet**, and in the Data Sources. Click on the drop arrow on the Faculty table combo box and select the **Details** item, and drag this **Details** item and place it into the Form, as shown in Figure 2.52.

![](img/d59a47501d0a20fc0460a49c469c6fb7_76_1.png)

**2.52** Drag and drag three columns in dataset format for faculty table.
