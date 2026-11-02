to describe each page and its behavior. We'll see this in—you guessed it—Chapter 3.

In this model, default.html is little more than a simple container, with everything else in the app coming through subsidiary pages. The Navigation template creates only one subsidiary page, yet it establishes the framework for how to work with multiple pages. Additional pages are easily added to a project through a page item template (right click a folder in your project in Visual Studio and select Add > New Item > Page Control).

# # Grid App Template

> *A three-page project for a Windows Store app that navigates among grouped items arranged in a grid. Dedicated pages display group and item details.* (Blend/Visual Studio description)

Building on the Navigation template, the Grid template provides the basis for apps that will navigate collections of data across multiple pages. The home page shows grouped items within the collection, from which you can then navigate into the details of an item or into the details of a group and its items (from which you can then go into individual item details as well).

In addition to the navigation, the Grid template also shows how to manage collections of data through the `WinJS.Binding.List` class, a topic we'll explore much further in Chapter 7, “Collection Controls.” It also provides the structure for an app bar and shows how to simplify the app's behavior in narrow views.

The name of the template, by the way, derives from the particular grid *layout* used to display the collection, not from the CSS grid.

# # Hub App Template

> *A three-page project for a Windows Store app that implements the hub navigation pattern by using a hub control on the first page and provides two dedicated pages for displaying group and item details.* (Blend/Visual Studio description)

Functionally similar to a Grid Template app, the Hub template uses the `WinJS` Hub control for a home page with heterogeneous content (that is, where multiple collections could be involved). From there the app navigates to group and item pages. We'll learn about the Hub control in Chapter 8.

# # Split Template

> *A two-page project for a Windows Store app that navigates among grouped items. The first page allows group selection while the second displays an item list alongside details for the selected item.* (Blend/Visual Studio description)

This last template also builds on the Navigation template and works over a collection of data. Its home page displays a list of groups, rather than grouped items as with the Grid template. Tapping a group navigates to a group detail page that is split into two sides (hence the template name). The left