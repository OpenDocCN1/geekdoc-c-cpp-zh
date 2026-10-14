# # How to work in Source and Split views

As you design a form in Design view, HTML and asp tags are being generated in Source view. This is the code that’s used to render the web page that’s sent to the user’s browser. What you see in Design view is just a visual representation of that code. In many cases, you’ll need to work in Source view to get a page to look just the way you want it to. When you work in Source view, you can also use a new feature of Visual Studio for ASP.NET called code snippets. You may also want to work in Split view so you can see both Design view and Source view at the same time.

# ## How to use Source view to modify the design

As you saw in the last chapter, HTML consists of tags. For instance, the `<form>` and `</form>` tags mark the start and end of the HTML code for a web form. And the `<table>` and `</table>` tags mark the start and end of the HTML code for a table.

In addition to the HTML tags, ASP.NET adds asp tags for the web server controls that are added to the form. In figure 2-11, you can see some of the asp tags for the Future Value form. For instance, the `<asp:DropDownList>` and `</asp:DropDownList>` tags mark the start and end of the code for a drop-down list. Within these tags, you’ll find the code for the property settings of the controls. Note, however, that all of this asp code is converted to HTML before the page can be sent to a browser, because a browser can only interpret HTML.

Because the file that contains the source code for a web form has an aspx extension, we refer to the source code for a form as *asp code*. This also indicates that the code contains both HTML and asp tags.

In case you need it, chapter 5 presents a crash course in HTML. In the meantime, though, you may be surprised to discover how easy it is to modify the design of a form by adjusting the aspx code using the *HTML Editor*.

To start, you can enter a title for the form between the `<title>` and `</title>` tags near the top of the source code. This is the title that’s displayed in the title bar of the browser when the form is run (see figure 2-6). In this example, the title is “Chapter 2: Future Value.” As you will see, all of the applications in this book have titles that indicate both the chapter number and the type of application.

You can also change the text that has been entered into a form or some of the settings for HTML elements. If, for example, you want to change the text in the first row of the table from “Monthly investment” to “Investment amount,” you can just edit the text in Source view. And if you want to modify the color for the heading, you can do that too. As you edit, just follow the syntax of the other entries, which will be easier to do after you read chapter 5.

To change the properties of a server control, you can click in the starting asp tag to select the control. Then, you can use the Properties window just as if you were in Design view. When you change a property, the *attribute* that represents the property in the asp tag for the control is changed. You can also change the