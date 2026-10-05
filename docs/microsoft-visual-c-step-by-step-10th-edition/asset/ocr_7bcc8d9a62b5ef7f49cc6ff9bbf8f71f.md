thinks an earlier call failed or timed out, because the result could be multiple
dplicated credits to the same account.

For more information about managing data consistency in cloud
applications, see “Data Consistency Primer” at
https://msdn.microsoft.com/library/dn589800.aspx.

Many modern applications don’t provide any functionality to delete certain
types of data. For example, in the Customers app, you might want to ensure that
you have a record of all customers who have done business with the Adventure
Works organization, which might be required for auditing purposes. Additionally,
even if a customer hasn’t been active for a long time, there’s a chance that the
customer might place an order at some point in the future. it’s becoming
increasingly commonplace for business applications never to delete data,
simple to perform an update that marks the data as removed in some way and
prevents it from being displayed. This is primarily because of the requirements to
keep complete data records, often to meet regulatory requirements.

Sadly, time and space does not permit a detailed discussion how to
implement insert and edit functionality in the Customers app. Suffice to say that
y need to implement additional modes in the ViewModel (adding and editing)
and create commands that invoke the relevant methods in the web service.
However, a complete working version of the app that enables you to create
and update customers is available in the sample code supplied with this book.
Look in the \Microsoft Press\VCSBS\Chapter 27\Web Service\Customers with
Insert and Update Features located in your Documents folder.

# Summary

In this chapter, you learned how to use the Entity Framework to create an entity
model that you can use to connect to a SQL Server database. The database can be
running locally or in the cloud. You also saw how to create a REST web service
that UWP app can use to query and update data in the database through the entity
model. Finally, you learned how to integrate code that calls the web service into a
ViewModel.

You have now completed all the exercises in this book. I hope you’re
thoroughly conversant with the C# language and understand how to use Visual
Studio 2022 to build professional apps for Windows 11. However, this is not the