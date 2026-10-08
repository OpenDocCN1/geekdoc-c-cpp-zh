# Chapter 22 Databases LINQ

+   22.1 Introduction
22.2 Relational Databases
22.3 A Books Database
22.4 LINQ to Entities and the ADO.NET Entity Framework
22.5 Querying a Database with LINQ
22.5.1 Creating the ADO.NET Entity Data Class Library
22.5.2 Creating Windows Forms Project and Configuring It to Use the Entity Data Model
22.5.3 Data Bindings Between Controls and the Entity Data Model
22.6 Dynamically Binding Query Results
22.6.1 Creating the Display Query Results GUI

+   22.6.2 Coding the Display Query Results App
22.7 Retrieving Data from Multiple Tables with LINQ
22.8 Creating a Master/Detail View App
22.8.1 Creating the Master/Detail GUI
22.8.2 Creating the Master/Detail Detail App
22.9 Address Book Case Study
22.9.1 Creating the Address Book App's GUI
22.9.2 Creating the Address Book App
22.10 Tools and Web Resources
22.11 Wrap-Up

Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# 22.1 Introduction

a database is an organized collection of data. A database management system (DBMS) provides mechanisms for storing, organizing, retrieving and modifying data. Many of today's most popular DBMSs manage relational databases, which organize data simply as tables with rows and columns.

Some popular DBMSs are Microsoft SQL Server, Oracle, Sybase and IBM DB2. PostgreSQL, MariaDB and MySQL are open-source DBMSs that can be downloaded and used freely. In this chapter, we use a version of Microsoft's SQL Server that is installed with Visual Studio. It can also be downloaded separately from

> https://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/sql-server-express.aspx

# SQL Server Express

SQL Server Express provides many features of Microsoft's full (fee-based) SQL Server product, but has some limitations, such as a maximum database size of 10GB. SQL Server Express database file can be easily migrated to a full version of SQL Server. You can learn more about the SQL Server versions at

> https://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/overview.aspx

The version of SQL Server bundled with Visual Studio Community is called SQL Server Express LocalDB. It's meant for development and testing of apps on your computer.

# Structured Query Language (SQL)

A language called Structured Query Language (SQL)—pronounced “sequel”—is an international standard used with relational databases to perform queries that request information satisfies given criteria and to manipulate data. For years, programs that