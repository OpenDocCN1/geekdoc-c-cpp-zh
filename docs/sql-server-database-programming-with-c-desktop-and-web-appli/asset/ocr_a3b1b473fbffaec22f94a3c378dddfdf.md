# Introduction to Databases

| course_id | course | faculty_id | faculty_name | phone |
|---|---|---|---|---||
| CSC-131A | Computers in Society | MTC-109 | A52990 | Black Anderson | 750-338-9987 |
| CSC-131B | Computers in Society | MTC-114 | B66750 | Alice Brown | 750-330-6650 |
| CSC-131C | Computers in Society | MTC-109 | A52990 | Black Anderson | 750-338-9987 |
| CSC-131D | Computers in Society | MTC-109 | B86590 | Davis Bhalla | 750-378-1061 |
| CSC-131E | Computers in Society | MTC-301 | B66750 | Alice Brown | 750-330-6650 |
| CSC-131I | Computers in Society | MTC-109 | A52990 | Black Anderson | 750-378-9987 |
| CSC-132A | Introduction to Programming | MTC-303 | J33486 | Steve Johnson | 750-330-1116 |
| CSC-132B | Introduction to Programming | MTC-302 | B78880 | Ying Bai | 750-378-1148 |

FIGURE 2.18 The old table.

| course_id | course | classroom |
|---|---|---||
| CSC-131A | Computers in Society | MTC-109 |
| CSC-131B | Computers in Society | MTC-114 |
| CSC-131C | Computers in Society | MTC-109 |
| CSC-131D | Computers in Society | MTC-109 |
| CSC-131E | Computers in Society | MTC-301 |
| CSC-131I | Computers in Society | MTC-109 |
| CSC-132A | Introduction to Programming | MTC-303 |
| CSC-132B | Introduction to Programming | MTC-302 |

FIGURE 2.19 The new table.

| faculty_id | faculty_name | phone |
|---|---|---||
| A52990 | Black Anderson | 750-378-9987 |
| B66750 | Alice Brown | 750-330-6650 |
| A52990 | Black Anderson | 750-378-9987 |
| B86590 | Davis Bhalla | 750-378-1061 |
| B66750 | Alice Brown | 750-330-6650 |
| A52990 | Black Anderson | 750-378-9987 |
| J33486 | Steve Johnson | 750-330-1116 |
| B78880 | Ying Bai | 750-378-1144 |
| A77587 | Debbie Angel | 750-330-2276 |

FIGURE 2.20 The new instructor.

# 2.8  DATABASE COMPONENTS IN SOME PUBLIC DATABASES

All databases allow for the storage, retrieval, and management of data. Simple databases provide basic services to accomplish these tasks. Many database providers, such as Microsoft SQL Server and Oracle, provide additional services which necessitates storing more data than other type databases. These components, such as views, stored procedures etc., are collectively called database objects.

There are two major of databases: File Server and Client Server:
In a File database, data is stored in a file and each user of the database retrieves the data, displays it, or modifies the data directly or from the file. In a Client Server database, the data is also stored in file; however, all operations are mediated through a master program called a server. MS Access is a File Server database, where Microsoft SQL Server and Oracle are