The RedirectToAction() method is used if no product is located and does exactly what its name suggests — it redirects the user to another view, in this case the Index view.

To add the new view, right-click on the Details() method and, as before, click the Add View . . . menu item. This time, create a strongly typed view for the Product class with Details view content, as shown in Figure 42-13.

Now when you run the application, you will be able to navigate to the products list through the Products menu item added in the previous section and view the details for any item, as shown in Figure 42-14.

![](bbox=[0.52, 0.13, 0.92, 0.38])

FIGURE 42-13

![](bbox=[0.13, 0.45, 0.75, 0.78])

FIGURE 42-14

If you manually edit the URL to an ID for a nonexistent product, you will be redirected to the product listing.

# Adding Items with Create()

There are two actions associated with creating new items, which are currently defined in code as follows:

```
public ActionResult Create()
{
    return View();
}
```