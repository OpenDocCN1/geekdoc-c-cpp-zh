ServiceControllerInfo contains an embedded ServiceController that is set with the constructor of the ServiceControllerInfo class. There is also a read-only property Controller to access the embedded ServiceController:

```
public class ServiceControllerInfo
{
    private readonly ServiceController controller;

    public ServiceControllerInfo(ServiceController controller)
    {
        this.controller = controller;
    }

    public ServiceController Controller
    {
        get { return controller; }
    }
}
```

code snippet ServiceControl/ServiceControllerInfo.cs

To display current information about the service, the ServiceControllerInfo class has the read-only properties DisplayName, ServiceName, ServiceTypeName, and ServiceStatusName. The implementation of the properties DisplayName and ServiceName just accesses the properties DisplayName and ServiceName of the underlying ServiceController class. With the implementation of the properties ServiceTypeName and ServiceStatusName, more work is done — the status and type of the service cannot be returned that easily because a string should be displayed instead of a number, which is what the ServiceController class returns. The property ServiceTypeName returns a string that represents the type of the service. The ServiceType you get from the property ServiceController.ServiceType represents a set of flags that can be combined by using the bitwise OR operator. The InteractiveProcess bit can be set together with Win32OwnProcess and Win32ShareProcess. So, first it is checked if the InteractiveProcess bit is set before continuing to check for the other values. With services, the string returned will be “Win32 Service Process” or “Win32 Shared Process”:

```
public string ServiceTypeName
{
    get
    {
        ServiceType type = controller.ServiceType;
        string serviceTypeName = "";
        if ((type & ServiceType.InteractiveProcess) != 0)
        {
            serviceTypeName = "Interactive ";
            type -= ServiceType.InteractiveProcess;
        }
        switch (type)
        {
            case ServiceType.Adapter:
                serviceTypeName += "Adapter";
                break;

            case ServiceType.FileSystemDriver:
            case ServiceType.KernelDriver:
            case ServiceType.RecognizerDriver:
                serviceTypeName += "Driver";
                break;

            case ServiceType.Win32OwnProcess:
                serviceTypeName += "Win32 Service Process";
                break;

            case ServiceType.Win32ShareProcess:
```