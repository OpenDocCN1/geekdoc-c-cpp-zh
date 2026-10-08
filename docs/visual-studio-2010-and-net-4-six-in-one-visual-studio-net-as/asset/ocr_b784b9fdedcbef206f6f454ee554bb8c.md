Even if you implement validation at the client side, you must not trust only client-side validation. Robust business logic should check all business rules at the server (service) as as well.

# UI Customization

The Add View command (available in the context menu of the code editor, or from the Solution Explorer) helps you generate a view in a few seconds. This may be short, and easy to work with, not necessarily the one you would like to put into the live version of your application. The ASP.NET MVC 2 Framework provides many ways to define the UI according to your style and using the standard design of your company or customers.

In the Views/Shared folder, you can see that the Site.Master page and the Content folder hold the Site.cs file. You can use the same techniques as any other ASP.NET application to change your application's general output by changing/adding master files and CSS files. Because of the pernicious structure of these files, a practiced web designer can create awesome and attractive web sites for your MVC 2 application.

However, there are other ways you can customize the views in your application.

# Using Templated Helpers

MVC 2 has a new feature called template helpers, probably the most important feature for developer productivity. Earlier in this chapter, the source code listings of views, you may see several rendering tags that were not explained, such as the following:

```
<@ using (Html.BeginForm()) %>
<%= Html.LabelFor(model = model.Author) %>

<%= Html.TextBoxFor(model = model.Title) %>
<%= Html.ValidationMessage(model = model.Title) %>

<%= Html.ActionLink("Back to List", "Index") %>
```

The magical object that has the LabelFor, TextBox, and other methods are invoked in the System.Web.Mvc.PageView class derives the views from. It is type HtmlHelper, which has many methods and extension methods (defined in a dozen classes). With these extensions, you can get rid of creating HTML tags on your own. Actually, thisHelper methods help you with the following services:

+   - They know how to generate HTML output for native or compound HTML controls, including their attributes.
- They can query the metadata belonging to your model, and this information when generating the code for the view.

These methods work a bit trickier than they look. For example, the LabelFor method accepts a function that projects a model to a property. In the previous snippet, a lambda expression