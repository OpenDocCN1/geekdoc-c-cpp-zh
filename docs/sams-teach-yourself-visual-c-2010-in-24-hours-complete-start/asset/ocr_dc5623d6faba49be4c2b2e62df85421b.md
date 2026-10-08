web server that contains the web application. The second line tells the ASP.NET run-time engine to actually perform the binding. Now you need to add the binding expressions to the user interface controls, as shown in Listing 19.8.

# LISTING 19.8 Adding Binding Expressions

```
<asp:HyperLink runat="server" ID="h1Item"
    NavigateUrl='<%# Eval("Name", "viewAlbum.aspx?id={0}") %>'
    Text='<%# Eval("Name") %>' />
<br>
<asp:Label runat="server" ID="1b1Item"
    Text='<%# Eval("Count", "{0} pictures") %>' />
```

The Eval method takes the name of a data field in the current data item and, optionally, a formatting string used to display the data. This formatting string uses the same formatting syntax as the String.Format method. Notice that you don't specify the container (or data context) of the binding. That's because the Eval method uses the naming container, which is generally the smallest part of the data-bound control that contains a whole record. As a result, you can use only Eval for binding expressions inside templates of a data-bound control like a DataList.

# Embedded ASP.NET Code Blocks

The <% %> tags indicate embedded code blocks, which is server code that executes during the page's render stage. If the Page directive includes the Language attribute, the embedded code must be written using the indicated language. The common types of embedded code block follow:

+   - \`%>\`—The simplest form of embedded code block that can contain any code
- \`%@ \`—Directives
- \`<%# \`—Data binding expressions
- \`<%= \`—Used to write text data to the page, the equivalent of `<%= Response.Write() %>`
- \`<%\`—Server-side comments

If you need to use data binding in another control, you can still do so by using the DataBinder.Eval method directly. In fact, the binding expressions you just saw internally call DataBinder.Eval and pass Container.DataItem, which refers to the current data item of the current data container, as the first parameter.

You could rewrite the binding expression for the Label control as shown here:

```
<%# DataBinder.Eval(Container.DataItem, "Count", "{0} pictures") %>
```

> By the Way