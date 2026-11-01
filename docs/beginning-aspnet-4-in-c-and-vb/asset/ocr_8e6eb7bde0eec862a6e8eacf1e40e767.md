arrive within a specified time. This workflow then has a number of periods of execution, and other times when it is dormant and could be unloaded from memory. Before being unloaded, however, it is necessary to define a point in the workflow where processing can be resumed, and this is where bookmarks are used.

To define a bookmark, you need a custom activity that derives from NativeActivity. You can then create a bookmark within the Execute method, and when the bookmark has been resumed your code will continue. The example activity below defines a simplistic Task activity that creates a bookmark, and on resumption at the point of that bookmark, the activity completes.

```
```csharp
public class Task : NativeActivity<Boolean>
{
    [RequiredArgument]
    public InArgument<string> TaskName { get; set; }

    protected override bool CanInduceIdle
    {
        get { return true; }
    }

    protected override void Execute(NativeActivityContext context)
    {
        context.CreateBookmark(TaskName.Get(context),
            new BookmarkCallback(OnTaskComplete));
    }

    private void OnTaskComplete(NativeActivityContext context,
        Bookmark bookmark, object state)
    {
        bool taskOK = Convert.ToBoolean(state);
        this.Result.Set(context, taskOK);
    }
}
```
```

code download 06_WorkflowApplication

The call to CreateBookmark passes the name of the bookmark and also a callback function. This callback will be executed when the bookmark is resumed. The callback itself is passed an arbitrary object, which in this case is a Boolean, as we've decided that each task should report success or failure, and we can then use this to decide on the next steps in the workflow — it could be a complex type with many fields.

So that's the activity written — we now need to alter the hosting code so as to resume at the point of the bookmarks. But there's another problem — how does the hosting code know that a workflow has created a bookmark? If it's the host's responsibility to resume from the bookmark, it needs to know that one exists.

The Task we've created above really needs to do some more work — telling the outside world that a task has been created. In a production system, this would typically result in an entry being stored in a queue table, and this queue would be presented to the call center staff as a job list.

Communicating with the host is the subject of the next section, “Extensions.”

# Extensions

An extension is simply a class or interface that is added to the runtime context of a workflow application. In Workflow 3.x these were called Services, however that clashed with WCF Services, so these have been renamed extensions in Workflow 4.

You will typically define an interface for your extensions and then provide a runtime implementation of this interface. Your activities will simply call the interface, and this allows the implementation to change as necessary. A good example of an extension is something that sends an e-mail. You could create a SendEmail