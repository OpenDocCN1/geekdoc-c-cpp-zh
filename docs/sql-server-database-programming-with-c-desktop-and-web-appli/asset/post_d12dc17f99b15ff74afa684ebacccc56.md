
# Accessing Data in ASP.NET

H. A cleaning job is performed to clean up the contents of all textboxes that stored the deleted faculty information.

I. The deleted image is also removed from the PhotoBox object in this page.
J. The user-defined method getCurrent() is called to query the Faculty table to get updated faculty names, and display them in the Faculty Name combobox.

At this point, we have finished all coding to delete data against the SQL Server database via Web Pages. Before we can run the project to test this deleting function, make sure that the page is the Loginpage.

After the project, enter the suitable username and password to complete the login process, then open the Faculty page by clicking the Faculty Information from the Selection page, select the default faculty Ying Bai from the combobox and click the Select button to retrieve and display the faculty information.

Now click on the Delete button to delete this faculty record from our database. Immediately, all seven pieces of faculty information stored in the related textboxes are removed. The selected faculty image is also removed.

To confirm this deleting, opening the Faculty Name combobox, and the deleted faculty member, Ying Bai, cannot be found from this, which means that this faculty has been deleted from our sample database.

Another way to confirm this deleting is to open our sample database via the Microsoft SQL Management Studio 18, and you can find all records related to deleted faculty member, Ying Bai, as shown in Figures 8.49-8.52, have been deleted from our database. Yes, our data deleting action is successful.

Before we close the SQL Server Management Studio, it is highly recommended that you recover all records that have been deleted from our sample database. To do recovering job, you need to take the following actions in the orders:

- 1) Recover the Faculty by inserting the deleted faculty record, which is shown in Figure 8.49, into the Faculty table using the Insert button on this Faculty page.
- 2) Recover the login table by adding the deleted login record, as shown in Figure 8.50, into the login table via the Microsoft SQL Management Studio.

| faculty_id | faculty_name | office | college | title | email | fimage |
| --- | --- | --- | --- | --- | --- | --- |
| B78880 | Ying Bai | MTC211 | 750-378-1148 | Florida Atlantic University | Associate Professor | ybai@college.edu | Bai.Jpg |

FIGURE 8.49 The deleted data from the faculty table.

| user_name | pass_word | faculty_id | student_id |
| --- | --- | --- | --- |
| ybai | come | B78880 | NULL |

FIGURE 8.50 The deleted data from the Login table.

| course_id | course | credit | classroom | schedule | enrollment | faculty_id |
| --- | --- | --- | --- | --- | --- | --- |
| CSC-132B | Introduction to Programming | 3 | MTC-302 | T-H: 1:00-2:25 PM | 21 | B78880 |
| CSC-234A | Data Structures & Algorithms | 3 | MTC-302 | M-W: 9:00-9:55 AM | 25 | B78880 |
| CSE-434 | Advanced Electronics Systems | 3 | MTC-213 | M-W: 1:00-1:55 PM | 26 | B78880 |
| CSE-438 | Advd Logic & Microprocessor | 3 | MTC-213 | M-W: 11:00-11:55 AM | 35 | B78880 |

FIGURE 8.51 The deleted data from the course.

| s_course_id | student_id | course_id | credit | major |
| --- | --- | --- | --- | --- |
| 1005 | T77896 | CSC-234A | | 3 CS/IS |
| 1009 | A78835 | CSE-434 | | 3 CE |
| 1014 | A78835 | CSE-438 | | 3 CE |
| 1016 | A97850 | CSC-132B | | 3 ISE |
| 1017 | A97850 | CSC-234A | | 3 ISE |

**Figure 8.52** The data deleted from the StudentCourse table.

- 3) Recover the *Course* table by adding the deleted course records, which are shown in Figure 8.51, in the *Course* table via the Microsoft SQL Management Studio 18.
- 4) Recover the *StudentCourse* table by adding the deleted courses by the associated students, as shown in Figure 8.52, into the *StudentCourse* table via the Microsoft SQL Management Studio 18.

When performing the first recovery job, one can use the **Insert** button and its Click method to perform another data insertion to insert deleted faculty record.
To recover jobs 2-4, one can use the Microsoft SQL Server Management Studio 18 to open our sample database and related tables, and add those records one by one. One can copy all rows from Figures 8.51 and 8.52, and paste them on the bottom of each related table.

A complete Web project **SQLUpdateDeleteProject** can be found from a folder Class DB Projects\$SQLUpdateDelete Solution that is located on the Students folder on the CRC Fps ftp site (refer to Figure 1.2 in Chapter 1).

# 8.7 DEVELOP .NET WEB APPLICATIONS WITH LINQ TO SQL QUERY

In this section, we provide a fundamental end-to-end LINQ to SQL scenario for selecting, adding, modifying, and deleting data against our sample database via Web pages. As you know, LINQ to SQL queries perform not only the selection, but also data insertion, and deleting. Standard LINQ to SQL queries includes

- Select
- Insert
- Update
- Delete

To perform any of these operations, we need to use entity classes and DataContext we discussed in Section 4.6.1 in Chapter 4 to LINQ to SQL actions against our sample database. We have already created a Windows-based application project **LINSelectProject** in Section 5.17.1 in Chapter 5 to illustrate how to use LINQ to SQL to perform queries against our **Login**, **Faculty**, and **Student** tables in our sample database. However, in this section, we want to create a Web-based project to perform the data selection, data insertion, data updating and deletions against related tables in our sample database **CSE_DEPT** using the LINQ to SQL via Web pages.
Now let's perform the following steps to create our new project **WebLINQSQL**:

- 1) a new ASP.NET Web Application (.NET Framework) C# project and set the Project name as WebLINQSQLProject and Solution name as WebLINQSQL, respectively. Select the C:\Chapter 8 as the location to save this project and click the **Create** button.
- 2) On the next wizard, select the **Web Forms** as the template, and click on the **Create** button again to create this project.

# Access Data in ASP.NET

- 3) On the new Web project, go to the Solution Explorer and select the **Default.aspx** by right clicking on it, and select the **Delete** item to remove it since we do not need this page in project, and we can use the **Login** page as our default or start page.

Next we need to add four Web pages in Sections 8.4.1, 8.4.5, 8.4.7 and 8.4.9 to this new project and add some reference to LINQ to SQL. Perform the following operations to complete these:

- 1) Right-click on our new project WebLINQSQL Project from the Solution Explorer, and select the **Add | Existing Item** item menu from the popup.
- 2) On the opened **Existing Item** window, browse to the folders **Web\Forms** that is located on the CRC Fcp path, select all of those pages with extensions, such as ***.aspx**, ***.designer.cs**, by checking each of them. (An example is **Login.aspx**, **Login.designer.cs** and **Login.designer.cs**). Then click the **Add** button to add them into our project. One can copy all of pages and save them to one of your local folders, and get them from that folder.
- 3) We need to add **System.Data.Linq** reference to this new project. Right-click on our new project from the Solution Explorer, and select **Add | Reference** item from the popup menu to open the Add Reference window. Select the default tab and scroll down the Reference List until you find the item **System.Data.Linq**, by checking the checkbox in front of it and click the **OK** button to add this reference to our project.

A point is be noted that all of those pages are generated under the namespace **SQLWeb_Project**, that cannot be changed unless we add them to our current project.

## 8.7.1 Create Entity Classes and Connect the DataContext to the Database

We need to create this new entity class of the DataContext class since we need to this object to connect to our sample database to perform data queries. In fact, we need first to create entity classes using **LINQ to SQL** tools provided by Visual Studio.NET to set mapping relationships between each physical data table and the related entity class. We prefer to use the Object Relational Designer which provides a graphical user interface.

We have provided detailed discussion about how to install LINQ to SQL tools in Section 5.17.1 in Chapter 5. Refer to that to get detailed descriptions for those tools and final installation for it if you have not installed.
We provided detailed discussion about how to create entity class and its object in Section 5.17.2 in Chapter 5. For your convenience, we redo this in this section to make it easy to be built and applied.

Perform the following operations to create this entity class and its object:

- 1) Right-click our project WebLINQSQL Project from the Solution Explorer, and select the **Add | New** item menu to open the Add New Item window.
- 2) On the opened window, select the **Visual C#** item then select the **LINQ to SQL Classes** item from the list by clicking on it, and enter **CSE_DEPT.dbml** in the **Name** box at the bottom as for this intermediate DBML file, as shown in Figure 8.53.
- 3) Then click the **Add** button to open this Object Relational Designer.

You can find that **CSE_DEPT.dbml** folder has been added into our project in the Solution Explorer window, which is shown in Figure 8.54. Two related files, **CSE_DEPT.dbml.layout** and **CSE_DEPT.designer.cs**,
