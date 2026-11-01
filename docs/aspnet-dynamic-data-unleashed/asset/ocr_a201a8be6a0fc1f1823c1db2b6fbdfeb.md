# NOTE

The EDMX files contain plain XML and work well with most modern source control systems. However, unless you are working on a trivial project with just a handful of tables and only one developer, eventually you will need to look at the EDMX in its raw XML form instead of relying on the Entity Designer. If you have multiple developers on your team, at some point you will need to merge the changes made by different developers at the same time, and even if you are the only developer working with the EDMX, it is always a good idea to review changes made by the Update Wizard in a large model before checking them in. For these reasons, it is important for developers to be familiar with the entity model XML schema, which is why some of its concepts are introduced here.

The *storage model* describes the database schema as it was captured by the Entity Designer last time when the Update Wizard was used to update model from the database. It includes definitions of tables and their foreign key relationships, as well as views and stored procedures. You can examine the storage model with the help of the Model Browser, a tool window you can open by right-clicking the surface of the Entity Designer and selecting Model Browser from the context menu. Figure 2.9 shows an example of the storage model definition of the Products table.

![](bbox=[0.12, 0.6, 0.43, 0.82])

FIGURE 2.9 Storage model.

The raw XML definition of the Products table looks similar to what's shown next. The Property elements define the individual columns, and Key element includes PropertyRef elements for all columns in the primary key: