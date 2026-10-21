# # Connecting to Data Sources

In this chapter, I will show you to how you can interface to a database using Visual C++ and the MFC and access the data from it. This is by no means a comprehensive discussion of the possibilities, because a full discussion of database application development using Visual C++ would occupy a very substantial book in its own right. In this chapter, however, you will look at how you can read from a database in this chapter, and in the next chapter you will explore the basics of how you can update a database. Of course, you can access data sources in CLR applications, and you'll look at this in Chapter 22.

+   In this chapter, you will learn about:
+   - SQL and how it is used
+   - How to retrieve data using the SQL SELECT operation
+   - What database services are supported by MFC
+   - What a recordset object is, and how it links to a relational database table
+   - How a recordset object can retrieve information from a database
+   - How a record view can display information from a recordset
+   - How to create a project for a database program
+   - How to add recordsets to your program
+   - How to handle multiple record views

# ## Database Basics

This is not the place for a detailed dissertation on database technology, but I do need to make sure that we have a common understanding of database terminology. Databases come in a variety of flavors but the majority these days are relational databases. It is relational databases that I will be talking about throughout this chapter.