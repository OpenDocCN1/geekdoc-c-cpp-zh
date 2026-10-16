```
public class EventListViewComponent : ViewComponent
{
    private readonly EventsAndMenusContext _context;
    public EventListViewComponent(EventsAndMenusContext context)
    {
        _context = context;
    }

    public Task<IViewComponentResult> InvokeAsync(DateTime from,
DateTime to)
    {
        return Task.FromResult<IViewComponentResult>(
            View(EventsByDateRange(from, to)));
    }

    private IEnumerable<Event> EventsByDateRange(DateTime from,
DateTime to)
    {
        return _context.Events.Where(e => e.Day >= from && e.Day <= to);
    }
}
```

The user interface for the view component is defined within the following code snippet. The view for the view component can be created with the item template MVC View Page; it uses the same Razor syntax. Specifically, it must be put into the Components/[viewcomponent] folder —for example, Components/EventList. For the view component to be available with all the controls, you need to create the Components folder in the Shared folder for the views. When you’re using a view component only from one specific controller, you can put it into the views controller folder instead. What’s different with this view, though, is that it needs to be named default.cshtml. You can create other view names as well; you need to specify these views using a parameter for the View method returned from the InvokeAsync method (code file MVCSampleApp/Views/Shared/Components/EventList/default.cshtml):

```
@using MVCSampleApp.Models;
@model IEnumerable<Event>

<h3>Formula 1 Calendar</h3>
<ul>
    @foreach (var ev in Model)
    {
        <li><div>@ev.Day.ToString("D")</div><div>@ev.Text</div></li>
    }
</ul>
```

Now as the view component is completed, you can show it by invoking the InvokeAsync method. Component is a dynamically created property of the view that returns an object implementing IViewComponentHelper. IViewComponentHelper allows you to invoke synchronous or asynchronous methods such as Invoke, InvokeAsync, RenderInvoke, and RenderInvokeAsync. Of course you can only invoke these methods that are implemented by the view component, and only use the parameters accordingly (code file MVCSampleApp/Views/ViewsDemo/UseViewComponent.cshtml):