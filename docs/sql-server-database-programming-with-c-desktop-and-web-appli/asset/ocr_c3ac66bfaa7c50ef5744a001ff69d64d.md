# SQL Server Database Programming with C#

![](bbox=[0.118, 0.09, 0.882, 0.345])

**5.110** The result of the nested stored procedure.

Enter a student name, such as Tom Erick, and click the OK button to run both stored procedures. The result is shown in Figure 5.110.

Our nested stored procedure work fine!
To call this stored procedure, we need to develop a Visual C# project. In order to save time and space, we can use the codes developed for the SP Form in the last sub-section. All codes are same and the only modification is the stored procedure's name declared in the cmdlet_Dcid() method, and the nominal input parameter name to stored procedure. Change the name of the stored procedure from dbo:StudentCourseINTO to dbo:StudentAndCourse (refer to line A in Figure 5.104), and change the nominal parameter's name from @StudentName to @StudentName (refer to line D) and you can run the project to get the same result, which is shown in Figure 5.107, as we got from project.

At this point, we are developing a data-driven project using the stored procedure for the SQL Server database. The class DcidProjects Chapter 5:SPSelect Solution is located on the Students folder in that site
Now let's go to the next part in this chapter – develop a data-driven application using the LINQ to SQL with the SQL Server database.

# 5.17 QUERY DATA USING THE LINQ TO SQL TECHNIQUE

As discussed in Chapter 4, LINQ to SQL is an application programming interface (API) that allows users to easily and conveniently access the SQL Server database from the Standard Query Operations (SQO) to relate to LINQ. To use this API, you must first setup a mapping relationship between your relational database and a group of objects that are instantiated from entity classes. The LINQ to SQL or the Standard Query Operators will interface with these classes to perform the real database operations. In other words, each entity can be mapped or is equivalent to a physical table in the database, and each entity class's property can be mapped or is equivalent to a data column in table. Only after this mapping relationship has been setup, can one use the LINQ to access and manipulate data against the connected databases.

After entity classes are created and a mapping relationship between each physical table and each entity class has been built, the conversion for data operations between the entity class and the real data table is needed. The class DataContext who will work in this. Basically the