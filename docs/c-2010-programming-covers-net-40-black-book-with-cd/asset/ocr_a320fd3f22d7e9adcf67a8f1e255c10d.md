Table 38.5 gives an overview of the structure of the Photos table:

| Table 38.4: The Items Table |
| Column Name | Data type | Allow Nulls | Description |
| Status | varchar(50) | No | Represents the status of the item |
| ImageUrl | varchar(50) | Yes | Specifies the name or location of the image that represents the item |

| Table 38.5: The Photos Table |
| Column Name | Data type | Allow Nulls | Description |
| PhotoID | int | No | Represents a unique ID for the photo |
| Name | varchar(50) | Yes | Represents the name of the photo |
| ImageUrl | varchar(100) | No | Specifies the name or location of the photo |

Table 38.6 gives an overview of the structure of the OrderDetails table:

| Table 38.6: The OrderDetails Table |
| Column Name | Data type | Allow Nulls | Description |
| OrderID | bigint | No | Represents a unique ID for the order |
| ItemsID | int | No | Represents the ID of the ordered item |
| Quantity | bigint | No | Represents the quantity of the ordered item |
| UserName | varchar(50) | No | Represents the name of the user |
| OrderDate | varchar(50) | No | Represents the ordered date |

Let’s now look at the development phase of this project.

# The Development and Testing Phase

After designing the structure of all the modules and the Sports database, you need to design the UIs and write the code for various Web pages using Microsoft Visual Studio 2010. At the back-end, Microsoft SQL Server 2008 is used to create the Sports database, which is used to store the data related to articles and items. The testing phase ensures proper functioning of the project. This phase checks the UIs and the functioning of the written code. In this phase, database connections that are created while developing the project are also checked.

# The Implementation and Maintenance Phase

The Implementation and maintenance phase is the last stage in the SDLC of a project. In this case, the Sports Website project becomes ready to be implemented in real environment where it can be used. The maintenance of the project implies that depending upon the users’ feedback and emerging requirements, a project can be updated from time-to-time.

Now, let’s summarize the main topics discussed in this chapter.

# Summary

This chapter discussed the case study of a sports company, which decided to create a website to cater to the demands of its increasing customers. The chapter further discussed the SDLC of a project and its various phases. You also learned to design and create different pages of the front-end interface of this project, such as Login, Articles, Shopping, and Gallery. Finally, different tables are designed to store the available data and information in the Sports database at the back-end of the project.

With this chapter, we come to the end of this book. All that remains is the implementation of all these C# 2010 technologies to work.