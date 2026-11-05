**Table 15-5** Additional Web Forms control classes (continued)

| Class identifier | Description |
|---|---|
| SiteMapPath | Displays a set of text or image hyperlinks that enable users to more easily navigate a Web site, while taking a minimal amount of page space |
| SqlDataSource | Represents a SQL database to data-bound controls |
| Table | Displays a table on a Web page |
| TreeView | Displays hierarchical data, such as a table of contents, in a tree structure |
| ValidationSummary | Displays a summary of all validation errors on a Web page, in a message box, or both |
| Xml | Displays an XML document |

The examples illustrated in this chapter specified the **File System** for the **Location** argument when the Web site was created. Moving the files to a different location and reopening the Web site is not as problematic as attempting to move a Web site created using **IIS**. You might find that after the Web site is opened and viewed in the browser, the IDE requests you to create a new solution file. However, it does that for you automatically.

# Web Services

Imagine including a link on your Web page to enable users to search the Web for a keyword. You could, of course, link to another page that has a search engine. But doing so takes the user away from your page. What if you want to keep the user at your page, but offer the same functionality as the large search engine sites? Or, what if you want to allow the user to learn the temperature for any city from your page? What if you want the user to obtain driving directions from his location to your location? If you do not want users to link to another site, but instead stay on your page and receive this data, you should explore adding a reference to a site that offers a Web Service method to do one or more of the previously described functions.

This is an age in which data is readily available but is often in different formats, so computers need to be able to share and use data from many different sources. In the simplest case, **Web services** enable you to exchange data from one computer to another over the Internet or an intranet. This exchange can involve the data being processed or manipulated before being sent. **Web services** are applications that return data. They actually constitute a unit of managed code that can be remotely executed using HTTP. Web services involve neither the presentation layer nor how the data is displayed after it is delivered to another computer. Web services are designed to transfer data in a usable format to another computer. Web services return unformatted data and it is up to the client to determine how the data is to be formatted or displayed.

The concept of **distributed computing**, in which applications are spread over more than one computer system, has been around for many years. Using Web services to communicate