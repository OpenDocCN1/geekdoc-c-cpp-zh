your favorite search engine and then search for ControlName Control MSD. For example, to find more information on the Wizard control you'd search for Wizard Control MSD. Typically, the MSD site is at the top of the search results.

# Other Standard Controls

This section briefly discusses the remainder of the controls in the Standard category of the Toolbox. You see many of them in the sample application in the rest of the book.

# LinkButton and ImageButton

The LinkButton and the ImageButton controls similarly to an ordinary Button control. Both of them cause a postback to the server when they are clicked. The LinkButton presents itself as a simple <a> element, puts back (using JavaScript) instead of requesting a new page. The ImageButton does the same, but displays an image that the user can click to trigger the postback.

# Image and ImageMap

These controls are pretty similar in that they display an image in the browser. The ImageMap enables you to define hotspots on the image that, either clicked, cause a postback to the server or navigate to a different page.

# Calendar

The Calendar control provides a rich interface that enables a user to select a date. You see more of it toward the end of this chapter when the ASP.NET state engine is discussed.

# FileUpload

The FileUpload control enables a user to upload files that can be stored on the server. You see more of this control in Chapter 14.

# Literal, Localize, and Substitute

All three controls look a like the Label control because they can display any static text or HTML. The biggest advantage of the Literal is that it renders no additional tag; it displays only what you assign to its Text property, and is very useful to display HTML or JavaScript that you build up in the Code Behind or that you retrieve from a database.

The Localize control is used in multilingual websites and is able to retrieve its contents from translated resource files. The Substitute control is used in advanced caching scenarios and enables you to update only parts of a page that is otherwise cached completely. Both of these controls fall outside the scope of this book, but for a good discussion of them you may want to get a copy of Wix's Professional ASP.NET 4.5 in C# and VB (ISBN: 978-1-118-33182-0).

# AdRotator

The AdRotator control enables you to display random advertisements on your website. The ads come from an XML file that you create over your server. Because lacks advanced features like click tracking and logging that are required in all but the simplest scenarios, this control isn't used much in today's websites.