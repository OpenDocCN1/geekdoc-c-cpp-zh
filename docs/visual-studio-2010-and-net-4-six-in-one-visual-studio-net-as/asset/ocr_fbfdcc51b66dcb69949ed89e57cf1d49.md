# TABLE 11-12 (continued)

| FILE | DESCRIPTION |
| --- | --- |
| App.xaml, App.xaml.cs | The main file of the WPF application, and its code-behind file. |
| DNRequest.edmx, DNRequest.Designer.cs | The ADO .NET entity data model of the request database. |
| MainWindow.xaml, MainWindow.xaml.cs | The main form of the application and its code-behind file. |
| RequestClientProxy.cs | A proxy class allowing the workflow instance access to the main form's functions. |

The project stores two kinds of data in its back-end database. It waits for the request approval, the states of workflow instances representing new requests are persisted into the database with the built-in SqlWorkflowInstanceStore. When a workflow instance completes, the related information is removed from the database. The requests are also stored in a user table (DNRequest). This table persists the request data even after the related workflow instance completes.

# The Main Workflow

The main workflow of the domain request process is implemented as a code-only workflow. It contains only a few activities constituting a sequence, as shown in Listing 11-11.

# LISTING 11-11: ProcessDomainNameRequest

```
using System.Activities;
using System.Activities.Statements;
using DomainNameDAL;

namespace RequestClient.Activities
{
    public sealed class ProcessDomainNameRequest: Activity
    {
        public InArgument<string> DomainName { get; set; }
        public ProcessDomainNameRequest()
    }

    var request = new Variable<DNRequest>("request");
    var status = new Variable<string>("status");
    Implementation =
    () =>
        new Sequence
        {
            DisplayName = "Process Domain Name Request",
            Variables =
            {
                request,
            }
```