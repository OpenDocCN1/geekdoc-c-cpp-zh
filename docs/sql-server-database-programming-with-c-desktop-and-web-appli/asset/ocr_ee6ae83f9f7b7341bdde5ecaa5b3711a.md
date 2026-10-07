# SQL Server Database Programming with C#

object. You can insert data into any data table by calling the ExecuteNonQuery() method that belongs to the Command class. We will concentrate on this method in part.

In this section, we provide a sample method RTOInsertProject to illustrate how to insert records into a SQL Server database using the runtime object method.

Now let's start to build the sample method RTOInsertProject to insert data into the SQL Server database using the runtime method. Recall in Sections 5.15.5, 5.15.6 and 5.16.3 in Chapter 5, we will discuss how to select data for the Faculty, Course and Form windows using the runtime object method. For the Faculty Form, a regular runtime selecting query is performed, and for the Student, the stored procedures are used to perform the runtime query.

We will concentrate on inserting data into the Faculty table from the Faculty Form window in this part.

In order to avoid duplication in the coding process, we will modify an existing project RTOSelect Project we developed in Chapter 5 to create our new RTOInsert Project used in this section.

# 6.5 INSERT DATA INTO THE SQL DATABASE USING THE RUNTIME OBJECT METHOD

Open the Windows Explorer and create a folder G\Chapter 6 if you have not yet done so. Then browse the folder DB Projects\Chapter 5\RTOSelect Solution that is located under the Students folder at the CRC press site, and copy the entire solution RTOSelect Solution to our new G\Chapter 6. Perform the following operational steps to make copied solution as our new solution and project:

+   1) Name the changes of the project from RTOSelect Solution to RTOInsert Solution, and RTOSelect Project to RTOInsert Project.
2) Change the project file name from RTOSelect Project.csproj to RTOInsert Project.csprojroj. Double-click on the RTOInsert Project.csprojroj to open this project.

+   1) Go to | RTOInsert Project Properties menu to open the project's property window. Change the Assembly name from RTOSelect Project to RTOInsert Project and the Default namespaces from RTOSelect_Project to RTOInsert_Project, respectively.
2) Click on the Assembly button to open the Assembly Information wizard, change the Title and Product to RTOInsert Project. Click on the OK to close this window.
3) Change the Startup object from RTOSelect_Project to (Not).
4) Go to the File | Save All menu to save those modifications. Click the Save button on the opened File explorer and Overwrite and save this project.
5) Right-click on the Login.cs folder in the Solution explorer and select the View Code item to open the solution and verify the Login.cs class file.
6) Change its namespace from the original RTOSelect_Project to our new namespace, RTOInsert_Project.
7) Open the Login.designer cs by double-clicking it from the Solution Explorer window (you need to expand the Login.cs to find this file).
8) Change the top line from the original namespace RTOSelect_Project to our current namespace, Selection.cs and Student.cs, to change the namespaces for all of those files.
9) Repeat steps 5–7 for all other files, such as Faculty.cs, Course.cs, Selection.cs