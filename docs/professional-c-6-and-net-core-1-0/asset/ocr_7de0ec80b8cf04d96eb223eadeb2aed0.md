request returns a partial view, and the result from the partial view is placed within the div element named events (code file MVCSampleApp/Views/ViewsDemo/UseAPartialView2.cshtml):

```
@model MVCSampleApp.Models.EventsAndMenusContext
@{
    ViewBag.Title ="Use a Partial View";
}
<script src="~/lib/jquery/dist/jquery.js"></script>
<script>
$(function () {
    $("#getEvents").click(function () {
        $("#events").load("/ViewsDemo/ShowEvents");
    });
});
</script>
<h2>Use a Partial View</h2>
<div>this is the main view</div>
<button id="FileName_getEvents">Get Events</button>
<div id="FileName_events">
</div>
```

# Working with View Components

ASP.NET MVC 6 offers a new alternative to partial views: view components. View components are very similar to partial views; the main difference is that view components are not related to a controller. This makes it easy to use them with multiple controllers. Examples of where view components are really useful are dynamic navigation of menus, a login panel, or sidebar content in a blog. These scenarios are useful independent of a single controller.

Like controllers and views, view components have two parts. With view components the controller functionality is taken over by a class that derives from ViewComponent (or a POCO class with the attribute ViewComponent). The user interface is defined similarly to a view, but the method to invoke the view component is different.

The following code snippet defines a view component that derives from the base class ViewComponent. This class makes use of the EventsAndMenusContext type that was earlier registered in the Startup class to be available with dependency injection. This works similarly to the controllers with constructor injection. The InvokeAsync method is defined to be called from the view that shows the view component. This method can have any number and type of parameters, as the method defined by the IViewComponentHelper interface defines a flexible number of parameters using the params keyword. Instead of using an async method implementation, you can synchronously implement this method returning IViewComponentResult instead of Task<IViewComponentResult>. However, typically the async variant is the best to use—for example, for accessing a database. The view component needs to be stored in a ViewComponents directory. This directory itself can be placed anywhere within the project (code file MVCSampleApp/ViewComponents/EventListViewComponent.cs):