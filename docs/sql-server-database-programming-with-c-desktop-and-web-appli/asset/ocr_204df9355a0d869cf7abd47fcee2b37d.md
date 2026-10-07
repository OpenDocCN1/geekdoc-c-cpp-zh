# SQL Server Database Programming with C#

| course_id | student_id | course_id | credit | major |
|---|---|---|---|---|
| 1002 | T77896 | CSC-335 | | CS/IS |
| 1005 | T77896 | CSC-234A | | CS/IS |
| 1010 | T77896 | CSC-439 | | CS/IS |
| 1015 | T77896 | CSC-432 | | CS/IS |
| 1020 | T77896 | CSE-439 | | CS/IS |
| 1024 | T77896 | CSC-333A | | CS/IS |

9.123 Deleted in StudentCourse table.

order: First recover the deleted record in the Student table since it is a parent table and the student_id is a primary key in that, and then do recover objects for other tables.
To recover the desired record in the Student table, especially for the student image column in the Student table, one can use Server Explorer and just enter a NULL to that column. One then performs another updating action by running this process by selecting the image file Erica.jpg with then can recover objects for the other child tables, Login and StudentCourse, by using the Server Explorer window.
A complete Web-based client project WebClientSQLUpdt Project can be found from a folder ClassBProjects\Chapter 9\WebClientSQLUpdt Solution that is under the Students folder located on the CRC ftp site (refer to Figure 1.2 in Chapter 1).
At this point, we have finished the discussion about how to access and manipulate data against the SQL Server database via ASP.NET services.

# 9.8 CHAPTER SUMMARY

A detailed discussion and analysis about the structure and components of the Web services are provided in this chapter. Unlike the ASP.NET Web applications, where the user needs to access the Web server through the client browser by sending requests to the server to obtain the desired information, the ASP.NET Web Services provide an automatic way to search, identify and return the desired information required by the user through a set of methods installed in the Web server, and those methods can be accessed by a computer program, not the user, via the Internet. Another important difference between the ASP-NET Web applications and ASP.NET Services is that the latter does not provide any graphical interfaces (GUIs) and users need to create those GUIs themselves to access the Web services via the Internet.
One of the most popular databases, SQL Server database, is discussed and used for three example Web projects:

+   * WebServiceSQLSelect.
* WebServiceSQLInsert.
* WebServiceSQLUpdateDelete.

Each Web service contains different Web methods that can be used to access different databases and perform the desired data actions as Select, Insert, Update and Delete via the Internet.
To consume Web services, different Web-based client projects are also developed in this chapter. Both Windows-based and Web-based client projects are discussed and built for each kind of Web service listed above. In total, nine projects, including the Web service projects and the associated Web service client projects, are developed in this chapter. All projects have been debugged and tested and can be run in any Windows-compatible operating systems such as Windows XP, Windows 7, and Windows 10.