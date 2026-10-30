
## Setting property values

You use the CurrentDb object’s CreateProperty and Properties.Append methods to add each of these properties. In most cases, unless the property has already been set in the Access Options dialog box, the property hasn’t been appended to the database’s Properties collection. You must make sure the property exists before trying to set its value in code. The following function sets the value of a startup property, creating and appending the property to the Properties collection if the property doesn’t exist:

```
Public Function SetStartupProperty(sPropName As String, _
 ePropType As DAO.DataTypeEnum, vPropValue As Variant) As Boolean

Dim db As DAO.Database
Dim prp As DAO.Property
Dim bReturn As Boolean

Set db = CurrentDb
On Error Resume Next
Set prp = db.Properties(sPropName)

If prp Is Nothing Then
Set prp = db.CreateProperty(sPropName, ePropType, vPropValue)

If prp Is Nothing Then
bReturn = False
Else
 db.Properties.Append prp
 bReturn = True
End If
Else
 prp.Value = vPropValue
 bReturn = True
End If

SetStartupProperty = bReturn

End Function
```

Using SetStartupProperty() is quite easy. You must know the exact property name and data type of the property before invoking SetStartupProperty(). The following subroutine demonstrates how to set a startup property with SetStartupProperty():

```
Sub ChangeAppTitle()

Dim bSuccess As Boolean

bSuccess = SetStartupProperty("AppTitle", dbText, "My Application")

If bSuccess Then
```

## Integrating Access with SharePoint

### IN THIS CHAPTER

- Getting familiar with SharePoint sites
- Understanding Access and SharePoint integration
- Linking to SharePoint lists
- Importing SharePoint lists
- Exporting Access tables to SharePoint
- Upsizing Access databases to SharePoint
- Using SharePoint list templates

Throughout this book you’ve read about the many features that Microsoft has added to Access over the years. As exciting and interesting as these new capabilities are, they pale in comparison to the ability to upsize Access applications to Windows SharePoint Server. Each recent version of Access has demonstrated greater and greater ability to integrate with SharePoint. The most exciting aspect of this integration is the ability to actually run your Access application as a SharePoint website.

In this chapter, we’ll explore the various techniques that allow you to upsize your Access databases to SharePoint. This chapter gives you an understanding of what SharePoint is and how it helps organizations share and collaborate data.

## Introducing SharePoint

SharePoint is Microsoft’s collaborative server environment, providing tools for sharing documents and data across various organizations within your company network.

SharePoint is typically deployed on a company’s network as a series of SharePoint sites. A SharePoint site is configured as an intranet site, giving various departments the ability to control their own security, workgroups, documents, and data. These sites can be nested within other sites in a hierarchical fashion.

## Part VII: Advanced Access Programming Techniques

As with any other website, the pages within a SharePoint site are accessible through a URL that the user can access via a standard web browser.

Although SharePoint is most frequently used for sharing documents, data tables, and other content management tasks, SharePoint is frequently applied to many other applications—for example, to handle the documentation required for product development. A SharePoint site devoted to a development project easily handles the project initiation, tracking, and progress reporting tasks. Because SharePoint easily handles virtually any type of document, project drawings, videos, schematics, photographs, and so on, can be added to the project’s SharePoint site for review and comment by project members.

Companies often use SharePoint for distributing human resource and policy documents. Because SharePoint provides user- and group-level security, it’s quite easy to grant a particular department access to a SharePoint page while denying other users access to the same page.

SharePoint also logs changes to documents and supports a check-in/check-out paradigm for controlling who is eligible to make changes to existing documents and who is allowed to post new documents and files.

Some of the most common SharePoint deployments are storing version-controlled documents, such as Word documents and Excel spreadsheets. In many environments, e-mail is used for passing documents back and forth between users. The potential for mixing up different versions of the same document is considerable. Also, storing multiple copies of the same document takes up a lot of disk space. Because SharePoint provides a single source for storing, viewing, and updating documents, many of these issues are eliminated entirely.

## Understanding SharePoint Sites

Before going into the detail of describing how Access integrates with SharePoint technology, it’s helpful to picture a typical SharePoint site. In this section, you’ll get a brief overview of the two most common aspects of a SharePoint site: documents and lists.

> **NOTE**
> 
> The topic of SharePoint is vast and worthy of its own book. In that light, we won’t be discussing how to create and manage SharePoint lists or document libraries. In this book, we’ll assume that your organization has a SharePoint site ready for consumption via Access. If you want to immerse yourself in SharePoint setup and administration, consider picking up the book *Beginning SharePoint 2013: Building Business Solutions with SharePoint*, by Amanda Perran, Sharyn Perran, Jennifer Mason, and Laura Rogers (Wiley, 2013).

## SharePoint documents

Perhaps the most common use of SharePoint is to store shared documents and other files. SharePoint keeps track of files from the moment they’re added to a list until they’re removed or deleted. Anyone with write-access to a SharePoint site can upload a document for sharing. Figure 32.1 shows a short list of several different types of files uploaded to a SharePoint document library.

### FIGURE 32.1

A SharePoint document library.

![](img/1e45673ab6eca9d20e67635ff5b9b318_1084_0.png)

In Figure 32.1, notice that the library contains several different types of documents. Each row in the document list includes an icon indicating the document’s type, the document’s name, the date it was last modified, and the name of the person who added the document to the list.

SharePoint document libraries support a check-in/check-out paradigm. Only one person at a time is able to check out a document for changes. Although not shown in Figure 32.1, SharePoint records when a document is checked in or out and keeps track of the individuals making changes. SharePoint can even be instructed to roll back document changes to an earlier version, if necessary.

Again, this document-sharing paradigm is most commonly used to share information across organizations, allowing for collaboration between the users of the SharePoint site.

## SharePoint lists

In addition to storing and tracking entire documents, SharePoint users can store and share data via SharePoint lists. SharePoint lists are conceptually similar to database tables in that each list consists of rows and columns of data. Each column holds a particular type of data, such as text, a date, or an object (such as a photo). From this simplistic perspective, SharePoint lists are analogous to Access tables.

### FIGURE 32.2

Figure 32.2 illustrates a typical SharePoint list. As you can see, the relevant information is presented in a single screen. You add a new item, edit an existing item, or delete an item through this same screen.

A SharePoint list allows for the storage and tracking of data in a table format.

![](img/1e45673ab6eca9d20e67635ff5b9b318_1085_0.png)

SharePoint can manage virtually any type of data you want to share with other people. Although the site shown in Figure 32.2 is designed for a specific purpose, SharePoint is suitable for many other scenarios. For example, an HR department could use a SharePoint list for sharing and tracking required training courses. An IT department could maintain a list of assets, including status and locations. Even smaller organizations like a local bowling club can share and maintain tournament schedules and player rankings as SharePoint lists.

SharePoint easily supports multiple lists, allowing an organization to add as many lists as needed. Unfortunately, unlike Access tables, SharePoint lists are not relational; there is no way to directly relate data in two different SharePoint lists or to query multiple SharePoint lists to find related data. However, SharePoint lists can be linked or imported into Access. Linking to SharePoint lists makes data stored on a SharePoint website appear as linked tables in Access.

For the most part, linking to a SharePoint list is no different from linking to a SQL Server database table or other remote data source. However, an important difference is that linked SharePoint lists in Access 2019 are read-only; you can’t edit or update the linked SharePoint list.
