# When to save and retrieve session state items

Most ASP.NET developers use session state in a consistent way. First, an application retrieves data from session state and stores it in variables. Then, the application uses these variables when it processes the user events. Finally, the application saves the updated variables back to session state so they can be retrieved the next time the page is posted back to the server.

If an item in session state is used within a single method in an application, you can retrieve, process, and save that item within that method. However, it’s more common for an application to use a session state item in two or more methods. Because of that, it makes sense to retrieve the item when the application first starts and save it just before it ends. To do that, you can use the Load and PreRender events of the page as shown in figure 8-4.

The example in this figure illustrates how this works. To keep this simple, this application consists of a single page that contains a Post button that the user can click to post the page back to the server. Each time the user clicks this button, the program code updates the label on the page to indicate how many times the button has been clicked.

To implement this application, a session state item named Count is used to maintain a count of the number of times the user clicks the Post button. To start, the Page_Load method sets a count variable to zero if the session state item named Count hasn’t been created yet. Otherwise, this method gets the value of the Count item from the session state object and assigns it to the count variable.

If the user clicked the Post button, the program executes the btnPost_Click method. This method adds one to the count variable and updates the label on the form to indicate how many times the button has been clicked.

Then, just before ASP.NET renders the HTML for the page, the Page_PreRender method is executed. This method saves the value of the count variable to session state so it’s available the next time the user clicks the Post button. Because PreRender is a page event, it’s raised each time the page is executed just like the Load event.

It’s important to note that the variable that’s used to store the value of the session state item in this example is a value-type variable. That means that the value is actually stored in the variable. Because of that, you have to explicitly update the session state item in the Page_PreRender method.

In contrast, if you use a reference-type variable such as a string or other object variable, the session state item is updated automatically when you update the variable that refers to it. That’s because the variable contains a pointer to the object, not the data itself. As a result, you don’t have to update the session state item explicitly. If you look back to the application in chapter 3, you’ll see that the Cart item in the session state object is handled that way.