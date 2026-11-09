(GUIs), to the design principles that drive good test design, to patterns of testing, and to some interesting and profound theoretical possibilities.

# # Testing Databases

The first rule of testing databases is: *Don’t test databases.* You don’t need to test the database. You can assume that the database works. You’ll find out soon enough if it doesn’t.

What you really want to test are queries. Or, rather, you want to test that the commands that you send to the database are properly formed. If you write SQL directly, you are going to want to test that your SQL statements work as intended. If you use an object-relational mapping (ORM) framework, such as Hibernate, you are going to want to test that Hibernate operates the database the way you intended. If you use a NoSQL database, you are going to want to test that all your database accesses behave as you intended.

None of these tests require you to test business rules; they are only about the queries themselves. So, the second rule of testing databases is: *Decouple the database from the business rules.*

We decouple them by creating an interface, which I have called `Gateway`¹ in the diagram in [Figure 4.1]. Within the `Gateway` interface, we create one method for every kind of query we wish to perform. Those methods can take arguments that modify the query. For example, in order to fetch all the `Employees` from the database whose hiring date was after 2001, we might call the `Gateway` method `getEmployeesHiredAfter(2001)`.

1. Martin Fowler, *Patterns of Enterprise Application Architecture* (Addison-Wesley, 2003), 466.