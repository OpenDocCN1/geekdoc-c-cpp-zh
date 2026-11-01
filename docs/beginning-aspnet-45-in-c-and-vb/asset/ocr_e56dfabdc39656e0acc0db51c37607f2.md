# FileUpload

The `FileUpload` control enables a user to upload files that can be stored on the server. You see more of this control in Chapter 14.

# Literal, Localize, and Substitute

All three controls look a little like the `Label` control because they can all display static text or HTML. The biggest advantage of the `Literal` is that it renders no additional tag itself; it displays only what you assign to its Text property, and is thus very useful to display HTML or JavaScript that you build up in the Code Behind or that you retrieve from a database.

The `Localize` control is used in multilingual websites and is able to retrieve its contents from translated resource files. The `Substitute` control is used in advanced caching scenarios and enables you to update only parts of a page that is otherwise cached completely. Both of these controls fall outside the scope of this book, but for a good discussion of them you may want to get a copy of Wrox's *Professional ASP.NET 4.5 in C# and VB* (ISBN: 978-1-118-31182-0).

# AdRotator

The `AdRotator` control enables you to display random advertisements on your website. The ads come from an XML file that you create on your server. Because it lacks advanced features like click tracking and logging that are required in most but the simplest scenarios, this control isn't used much in today's websites.

# HiddenField

The `HiddenField` control enables you to store data in the page that is submitted with each request. This is useful if you want the page to remember specific data without the user seeing it on the page. Because the field does show up in the HTML source of the page, and is thus accessible to the end user, you should never store any sensitive data in it.

# XML

The `XML` control enables you to transform data from an XML format to another format (like XHTML) for display on a page. Check out *Professional ASP.NET 4.5* for a detailed description.

# Table

The `<asp:Table>` control is in many respects identical to its HTML `<table>` counterpart. However, because the control lives at the server, you can program against it, creating new columns and rows dynamically and adding dynamic data to it.

This concludes the discussion of the controls in the Standard category of the Toolbox. In most web pages, you'll be working with at least a few of these controls. The remainder of this section discusses the other categories of the Toolbox. Because most of them are used in some form in the remainder of this book, this chapter just briefly describes their purpose so you get a rough idea what they are used for. You'll find cross-references to the other chapters where you can find out more information about them.