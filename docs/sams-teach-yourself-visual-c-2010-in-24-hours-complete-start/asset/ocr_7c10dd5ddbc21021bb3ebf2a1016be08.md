```
#MainContent_albums td span
{
    font-style:italic;
}
```

The declarations in the stylesheet starting with a dot (.) are CSS class definitions. The last style defined uses a combination of an ID selector and element selectors. This style indicates that it will be applied to any span elements that are children of any table cell (td element) in an element whose ID is MainContent_album.

# By the Way

> **Use Stylesheets Instead of Inline Styles**
Even though you can use inline styles instead of defining your CSS in a separate file (and can even mix them), you should use stylesheets as much as possible.
Inline styles are somewhat limited because you cannot easily build up styles, apply the same style to all instances of a certain element or to any element, or apply a style to an element with a specific name.
CSS stylesheets help to make your web application markup more maintainable and enable you to easily modify styles, even swapping stylesheets entirely to completely change the look of your web application.

# Understanding Data Binding

ASP.NET supports both one-way and two-way data binding in a way that is similar, although more limited, to that of WPF. The data-binding expressions are contained within <%# and %> delimiters and use either the Eval (one-way) or Bind (two-way) function. These expressions are resolved when the DataBind method of a control or Page class is called.

To make the page shown in Listing 19.3 useful, you need to provide text for the Labe1 control and both text and a navigation URL for the HyperLink control. This can easily be accomplished through data binding. The default page represents an album viewer and needs to be bound to an album collection. In the Page_Load method of Default.aspx.cs, add the code shown in Listing 19.7.

# **LISTING 19.7** Page_Load Method of Default.aspx.cs

```
albums.DataSource = new AlbumCollection(
    Path.Combine(Request.PhysicalApplicationPath, "Albums"));
albums.DataBind();
```

The first line creates a new AlbumCollection instance. The Request.PhysicalApplicationPath property represents the physical path on the