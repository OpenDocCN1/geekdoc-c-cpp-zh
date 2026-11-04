```
public string GetData(int value)
{
    return string.Format("You entered: {0}", value);
}

public CompositeType GetDataUsingDataContract(CompositeType composite)
{
    if (composite == null)
    {
        throw new ArgumentNullException("composite");
    }
    if (composite.BoolValue)
    {
        composite.StringValue += "Suffix";
    }
    return composite;
}
```

There are a few of things of interest here:

+   - **There is no [WebMethod] decoration.** You don't need it in WCF. The whole project is a service project.
+   - **The class implements a custom interface, IService.** We'll look at that in a second.
+   - **There are two sample methods.** The usual old "hello world" style method GetData, and a more complex example called GetDataUsingContract.

The GetDataUsingContract method makes a lot more sense when you take a look at IService.cs below.

```
namespace SHARPSERVICE
{
    // NOTE: You can use the "Rename" command on the "Refactor" menu to change
    the interface name "IService" in both code and config file together.
    [ServiceContract]
    public interface IService1
    {
        [OperationContract]
        string GetData(int value);

        [OperationContract]
        CompositeType GetDataUsingDataContract(CompositeType composite);

        // TODO: Add your service operations here
    }
    // Use a data contract as illustrated in the sample below to add composite
    types to service operations.
    [DataContract]
    public class CompositeType
    {
        bool boolValue = true;
        string stringValue = "Hello ";
    }
```