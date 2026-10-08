# Hosting the Service

To host the declarative service created earlier in this section, you can use the following code:

```
class Program
{
    static Service service;
    static void Main()
    {
        using (TextReader reader = File.OpenText("IWCFService.xml"))
        {
            service = (Service)XmlServices.Load(reader);
        }
        Uri address = new Uri("http://localhost:8000/IWCFService");
        WorkflowServiceHost host = new WorkflowServiceHost(service, address);
        try
        {
            host.Open();
            Console.WriteLine("Service started..press any key to stop.");
            Console.ReadLine();
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error occured: "+ex.Message);
        }
        finally
        {
            host.Close();
        }
    }
}
```

Note in the previous code snippet that the XAML file called IWCFService.xml is loaded using the File.OpenText(). Next, an instance of WorkflowServiceHost is created, and it is used to start the service by making a call to the Open() method. The ServiceHost class extends the ServiceBase class, and can be used to host workflow-based services. You can use this class to configure and expose a service so that it can be consumed by clients.

# Implementing the Service Logic Declaratively

The following code snippet illustrates how you can implement the service logic in XAML declaratively for the service created earlier:

```
<?xml version="1.0" encoding="utf-8" ?>
<Service
    xmlns="clr-namespace:System.ServiceModel"
    assembly=System.ServiceModelServiceModel"
    xmlns:wms="clr-namespace:System.WorkflowServiceModel"
    assembly=System.WorkflowServiceModel"
    xmlns:wm="clr-namespace:System.WorkflowServiceModel"
    Activities:assembly=System.WorkflowServiceModel"
    xmlns:wm="clr-namespace:System.WorkflowModel";
```