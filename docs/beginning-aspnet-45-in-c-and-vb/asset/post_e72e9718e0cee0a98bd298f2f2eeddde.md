
look at jQuery UI, a collection of widgets such as tabs, dialog boxes, calendars, draggable content, and more. You can find the jQuery UI project at http://jqueryui.com. If you like jQuery UI, you should also check out Juice UI (at http://juiceui.com). Juice UI is an open source collection of ASP.NET controls that render jQuery elements in the browser. This way, you get the best of both worlds: a rich and programmable framework at the server and lean and clean client-side HTML that leverages jQuery and jQuery UI.

Up until now, you've been working on fairly static web pages. Although jQuery enables you to create dynamically changing pages at the client, the content that's available on the website is still static. To fix that, you can use a database, the topic of the next four chapters. In the next chapter you get a thorough introduction to databases, and the chapters that follow give you in-depth information on working with data in an ASP.NET environment.

### PRACTICAL TIPS ON JQUERY

To get the most out of jQuery, follow these short tips:

- Experiment and experiment. At first, jQuery is a bit of an odd technique to master, mostly because of all its curly braces and parentheses. However, by practicing a lot you can become a jQuery master in no time.
- Visit the jQuery.com website. Besides very good documentation with many examples showing off jQuery's capabilities, you also find a wealth of articles and links on using jQuery, including links to sites that feature video content.
- Invest some time in browsing the jQuery UI and Juice UI websites. You may not need what they offer right now, or you may feel you're not ready to take that next step yet, but it's good to know what these products have to offer when you're building your next website with a rich client interface.

### SUMMARY

In this chapter you were introduced to jQuery, a very popular, open source, client-side JavaScript framework for interacting with the document object model.

The chapter started off by showing you where to get jQuery and how to add it to your site. You then got a quick example of jQuery, which was followed by an introduction to jQuery selectors and filters that enable you to find relevant elements in your page.

The second part of this chapter was devoted to the numerous methods that jQuery supports to apply effects and animations to your matched sets. You saw how to use methods like css to manipulate CSS settings, parent and prev to navigate through the items in your set, and how to work with events to fire code in response to some action like the click of a button or when a form is submitted.

Near the end of the chapter you learned how to use the many animation methods in jQuery to give your page a more compelling and interactive appearance, and you saw how to leverage the power of jQuery in the ASP.NET validation framework.

### WHAT YOU LEARNED IN THIS CHAPTER

| Term | Description |
|---|---|
| `_references.js` | The special JavaScript file in the Scripts folder that triggers IntelliSense for all JavaScript files it references |
| Chaining | The concept where the result of one method is used as the input of another to create a chain of effects |
| Filters | Enable you to further refine your jQuery matched set of elements |
| `Global.asax` | A central file that is used to handle various application-scoped events such as Application_Start, Application_Error, and more |
| jQuery | A popular client-side JavaScript framework that simplifies working with the DOM, visual effects, event handling, and Ajax functionality |
| Matched set | The set of elements that are returned by a jQuery selector |
| NuGet | The Library Package Manager for Visual Studio to help you manage third-party libraries in your .NET websites and projects |
| Selectors | A CSS-like syntax to find elements in your page using jQuery |

## 12 Introduction to Databases

### WHAT YOU WILL LEARN IN THIS CHAPTER:

- What a database is and which databases are typically used with ASP.NET pages
- What SQL is, how it looks, and how you use it to manipulate data
- What database relationships are and why they are important
- Which tools you have available to manage database objects (such as tables) and how to use them

### WROX.COM CODE DOWNLOADS FOR THIS CHAPTER

You can find the wrox.com code downloads for this chapter on the Download Code tab at www.wrox.com/remit.cgi?isbn=1118311809. The code is in the Chapter 12 download.

Being able to use a database in your ASP.NET websites is just as critical as understanding HTML and CSS: it's almost impossible to build a modern, full-featured website without it. Databases are useful because they enable you to store and retrieve data in a structured way. The biggest benefit of databases is that you can access them at run time in your site, which means you are no longer limited to just the relatively static files you create at design time in Visual Studio. You can use a database to store reviews, musical genres, pictures, information about users (usernames, e-mail addresses, passwords, and so on), log information about who reads your reviews, news articles, and much more, and then access that data from your ASPX pages.

This gives you great flexibility in the data you present, and the way you present it, enabling you to create highly dynamic websites that can adapt to your visitors' preferences, to the content your site has to offer, or even to the roles or access rights that your users have.

To successfully work with a database in an ASPX page, this chapter teaches you how to access databases using a query language called SQL—or Structured Query Language. This language enables you to retrieve and manipulate data stored in a database. You also see how to use the database tools to create tables and queries.

Although ASP.NET and the .NET Framework offer you many tools and technologies that enable you to work with databases without requiring a firm knowledge of the underlying concepts like SQL, it's still important to understand them. Once you know how to access a database, you'll find it easier to understand and appreciate other technologies, like the ADO.NET Entity Framework (discussed in Chapter 14), which provides easier access to database operations directly from code.

In the chapters that follow, you apply the things you learn in this chapter. In Chapter 13, you see how to use built-in controls to work with data in your database. In Chapter 14, you learn how to use the ADO.NET Entity Framework as an additional layer on top of your database to access data in an object-oriented way with minimal code. Chapter 15, the last of the data-focused chapters, shows you advanced techniques for working with data.

In the following sections, you see what a database is, and what different kinds of databases are available to you.

### WHAT IS A DATABASE?

By its simplest definition, a database is a collection of data that is arranged so it can be accessed, managed, and updated easily. For the purposes of this book, and the websites you will build, it's also safe to assume that the data in the database is stored in an electronic format.

The most popular type of database is the relational database. It's the type of database that is frequently used in websites and is also the type of database that is used in the remainder of this book. However, the relational database is not the only one. Other types exist, including flat-file, NoSQL, object-relational, and object-oriented databases, but these are less common in Internet applications.

A relational database has the notion of tables, where data is stored in rows and columns, much like a spreadsheet. Each row in a table contains the complete information about an item that is stored in the table. Each column, on the other hand, contains information about a specific property of the rows in the table.

The term "relational" refers to the way the different tables in the database can be related to each other. Instead of duplicating the same data over and over again, you store repeating data in its own table and then create a relationship to that data from other tables. Consider the table called Review in Figure 12-1. This table could store the album reviews that were presented on the Planet Wrox website.

![](img/eadab2ccd79b253c01a3fdff2321202d_467_0.png)

FIGURE 12-1
