
# WHAT YOU LEARNED IN THIS CHAPTER

| | |
|---||-|
| CRUD | The four basic SQL operations to work with data in a database: Create, Read, Update, and Delete |
| Foreign key | Identifies a column in a table that refers to the primary key of another table to enforce referential integrity |
| Identity | An automatic, sequential number assigned to new rows |
| JOIN | Enables you to express the relationship between two or more tables in a query to find related data |
| Primary key | Consists of one or more columns in a table that uniquely identify a row in that table |
| Relational database | A type of database where data is stored in separate, spreadsheet-like tables that can refer to each other |
| Relationship | Defines the relation between one or more tables and helps you enforce referential integrity |
| Table | An object in a database that enables you to store data |

# 13

## Displaying and Updating Data

WHAT YOU WILL LEARN IN THIS CHAPTER:

- How to display, insert, edit, and delete data using controls such as GridView, DetailsView, and DataSource
- How to create a rich interface that enables a user to insert and edit data while maintaining data integrity with the ASP.NET validation controls
- The best way to store your connection strings in your application so they are easily updatable

WROX.COM CODE DOWNLOADS FOR THIS CHAPTER

You can find the wrox.com code downloads for this chapter on the Download Code tab at www.wrox.com/go/beaspnet451. The code is in the Chapter 13 folder.

In this chapter you will learn how to display, insert, update, and delete data using the popular data controls that ship with ASP.NET. Besides working with the visual controls that are used to display and edit data in a web page, you also learn how to work with the SqlDataSource control that acts as the bridge between the database and ASPX pages.

The first things you need to look at are the available data controls, discussed in the next section.

## DATA CONTROLS

To enable you to work efficiently with the data in your system, ASP.NET offers two sets of data-aware controls: the data-bound controls and the data source controls.

The first group contains controls that you use to display and edit data, such as the GridView, Repeater, and ListView controls in the user interface. The data source controls are used to retrieve data from a data source, like a database or an XML file, and then offer data to the data-bound controls. Figure 13-1 shows the complete list of available data controls in the Data category of the Toolbox.

The following three sections provide a quick overview of all the controls in the Data category. In the remainder of this chapter you will get a much more detailed look at how these work and how to use them.

### Data-bound Controls

Seven of the controls in the Toolbox depicted in Figure 13-1 are the so-called data-bound controls. You use these to display and edit data on your web pages. The GridView, DataList, ListView, and Repeater are all to display multiple rows at the same time. As are also referred to as list controls. The DetailsView and the FormView are designed to show a single row at a time. The DataPager is a helper control used to provide paging capabilities to the ListView controls.

### List Controls

Because ASP.NET offers multiple controls to display lists

Figure 13-2 shows a typical GridView.

| Id | Title | CreateDateTime |
|---|---|---|
| Edit Edit Select | 17 | Sixteen Drum Bricks by Renato Cohen | 6/12/2009 12:52:53 PM |
| Edit Edit Select | 18 | Sounds Of The Universe by Depeche Mode - Overturned or a master piece* | 6/12/2009 10:10:12 PM |
| Edit Edit Select | 19 | First Album by Miss Kitty & The Hacker | 6/6/2009 08:50:38 PM |
| Edit Edit Select | 20 | Farm by Dinosaur Jr | 6/23/2009 10:36:01 PM |
| 1 2 3 4 5 6 | | |

FIGURE 13-2

The DataList control allows you to present data not only in rows with the GridView, but in columns as well, enabling you to create a matrix-like presentation of data. The control can be considered deprecated and is replaced with the ListView, which is a lot more powerful. As such, this book does not discuss the DataList any further.

![](img/9e033e3b9560597824f8b22941d6d8bb_477_0.png)

The Repeater gives you the greatest flexibility in terms of the HTML that you output to the browser because the control itself does not add any HTML to the page output, as it's often used for HTML ordered and unordered lists `<ol` and `<ul>` and other lists where you can't afford to have unwanted HTML mixed with your own. Define the entire markup with the numerous templates the control exposes. However, this flexibility comes at a price: the control has no built-in capabilities to sort, page, or modify data. You see more of the Repeater control in the next chapter.

The ListView was introduced in ASP.NET 3.5 and is a best-of-worlds combination of the GridView, the DataList, and the Repeater. It has undergone some changes in ASP.NET 4 and 4.5 that make it even easier to work with. The control supports editing, deleting, and paging of data, similar to the GridView. It supports multi-column and multi-row layouts like the DataList offers, and it enables you to completely control the markup generated by the control, just as the Repeater does. It also supports inserting and updating data like the DetailsView or FormView controls.

In ASP.NET 4, controls were extended with a ClientIDSuffix property allows you to indicate the column value you use to create unique client-side IDs based on the data. For this work, you need to set the ClientIDMode property that you saw in earlier chapters to Predictable.

In ASP.NET 4.5, the controls were extended with a new property: ItemType. You see this property at work in the next chapter.

### Single-item Controls

The DetailsView and FormView controls are somewhat similar in that both of them can display a single record at a time. The DetailsView uses a built-in tabular format to display data.

| Title | Love |
|---|---|
| Edit | --- |
| CreateDateTime | 6/12/2009 12:52:53 PM |
| Insert | 6/12/2009 10:10:12 PM |
| Edit | 6/6/2009 08:50:38 PM |
| Delete | 6/23/2009 10:36:01 PM |
| Summary | --- |

The DetailsView uses a built-in tabular format to display data. The data source controls are used to retrieve data from a data source, like a database or an XML file, and then offer data to the data-bound controls. Figure 13-1 shows the complete list of available data controls in the Data category of the Toolbox.

The following three sections provide a quick overview of all the controls in the Data category. In the remainder of this chapter you will get a much more detailed look at how these work and how to use them.

### Paging Controls

Another useful control is the DataPager, which enables paging on the ListView. For the time being, you can only use it to extend the ListView, but that might change with future versions of .NET.

### Data Source Controls

The Data category of the Toolbox contains six different data source controls that you can use to bind data to data-bound controls. The XmlDataSource and SiteMapDataSource are used to bind hierarchical, XML-based data to them. You will see MapDataSource when you created the site map in Chapter 7.

The ObjectDataSource control allows you to connect your data-bound controls to separate objects. Instead of tying data directly to a database, you bind data from a separate layer with custom objects to them. Get yourself a copy of Professional ASP.NET 4.5 (978-1-118-31821-0) if you want to find out more about the ObjectDataSource control.

The final three data source controls are the SqlDataSource, the EntityDataSource, and LinDataSource. The first is discussed in this chapter. The LinDataSource serves as a source for LINQ to SQL, a technology similar to the ADO.NET Framework you learned about.

Because Microsoft is now promoting the Entity Framework instead of LINQ to SQL, I won't discuss the LinDataSource control in this chapter. The EntityDataSource is used with older versions of the Entity Framework, and hasn't been updated for the latest version of EF. Instead of using this control, Microsoft recommends to use a concept called Model Binding, discussed extensively in the next chapter.

The QueryExtender control acts like an add-on to the LinDataSource and EntityDataSource controls in that it enables you to create a rich filtering interface to search for specific data without writing a lot of code. You can learn more about the QueryExtender in this article: http://bit.ly/92kMPQ.

The final control in the Toolbox is the Chart control. It was initially released as an add-on to VS 2008 but it's designed to render chart graphics from simple bar charts to 3D pie charts and line graphs. You won't discuss this control further, but you can find a series of articles that discuss it in detail here: http://tinyurl.com/nsnbvv.

In the next section you will see how to use the SqlDataSource and the GridView to retrieve and display data from a database.
