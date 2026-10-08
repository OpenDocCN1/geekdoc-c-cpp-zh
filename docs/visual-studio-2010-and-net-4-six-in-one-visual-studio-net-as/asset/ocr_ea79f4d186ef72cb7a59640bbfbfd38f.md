```
{ public sealed class CreateDomainNameRequest: CodeActivity {
    public InArgument<string> DomainName { get; set; }
    public OutArgument<DNRequest> Request { get; set; }

    protected override void Execute(CodeContext context) {
    using (var dataContext = new DomainNameDataEntities()) {
        var request = new DNRequest {
        WorkflowID = context.WorkflowInstanceId,
        RequestedName = DomainName.get(context),
        Status = "New"
    };
    dataContext.AddToToDNRequest(request);
    dataContext.SaveChanges();
    Request.Set(context, request);
}
}
```

Code file [CreateDomainNameRequest.cs] available for download at Wix.com

This activity is a CodeActivity, and its Execute method does the job. It accepts an input argument with DomainName of the requested domain, and it returns a DNRequest entity representing the request. The record is created and stored with the Entity Framework 4.0, where the related data context and the DNRequest entity are defined in DNRequest.edmx.

There is an especially important code line in Listing 11-12:

```
WorkflowID = context.WorkflowInstanceId
```

It saves the identifier of the current workflow instance into the WorkflowID field of the DNRequest record. The instance identifier is a GUID, and later, in this example, it will be used to resume the appropriate workflow instance when someone approves or denies the domain name request.

# Communicating with the Host Application

Two steps in the workflow are simple InvokeMethod activities that update the user interface. The first is run as soon as the request is queued; the second, when it is approved or denied. The workflow must communicate with the UI. It sounds as easy, but there are two issues to solve:

+   - The workflow instance must know the main window of the application (that is a singleton) in order to communicate with it.

+   - Any UI updates should happen in the UI thread.