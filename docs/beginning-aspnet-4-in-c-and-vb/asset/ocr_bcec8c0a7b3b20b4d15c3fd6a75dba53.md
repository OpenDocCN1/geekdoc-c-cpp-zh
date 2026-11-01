use. The first of the calls in the previous code snippet, for example, maps to the Index() method in the HomeController controller class.

When rendered with the default routing settings, these ActionLink() calls output the following HTML:

```
<div id="menucontainer">
<ul id="menu">
<li><a href="/">Home</a></li>
<li><a href="/Home/About">About</a></li>
</ul>
</div>
```

Given what you know about how the URLs map to controller methods, and how the defaults are set up for routing in Global.asax, this makes perfect sense. And the beauty is, you don't have to work these links out for yourself or rewrite them if routing changes.

To add a link to the product list page in the same way, add the following code to master page:

```
<div id="menucontainer">
<ul id="menu">
<li><%= Html.ActionLink("Home", "Index", "Home") %></li>
<li><%= Html.ActionLink("About", "About", "Home") %></li>
<li><%= Html.ActionLink("Products", "Index", "Products") %></li>
</ul>
</div>
```

*code snippet PCSMVC\MagicShop/Views/Shared/Site.Master*

The various overloads of ActionLink() enable you to do other things, such as pass parameters to a controller method. For example, in the product list view you created, the edit item link is rendered with the following code:

```
<%= Html.ActionLink("Edit", "Edit", new { id=item.ProductId }) %>
```

*code snippet PCSMVC\MagicShop/Views/Products/Index.aspx*

This overload uses linkText, actionName, and routeValues parameters (the controller name defaults to the current controller). In this case, a single route value of id is used, which maps to the id parameter of the Edit method in ProductsController. This call renders links, as shown in the following example HTML:

```
<a href="/Products/Edit/1">Edit</a>
```

# Viewing Items with Details()

The Details() action method in ProductsController is requested when a user clicks the Details link in the application. This results in the method being executed with the product ID passed as a parameter. All you need to do is to locate the requested product and, if it exists, return a new view, as follows:

```
public ActionResult Details(int id)
{
    var product = (from e in entities.Products
                    where e.ProductId == id
                    select e).FirstOrDefault();

    if (product != null)
    {
        return View(product);
    }
    else
    {
        return RedirectToAction("Index");
    }
}
```