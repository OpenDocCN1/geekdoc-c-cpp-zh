
```csharp
{
    [Import(AllowRecomposition=true)]
    ICustomerList CustomerRepository { get; set; }

    public ListingsWindow()
    {
        InitializeComponent();
    }

    public void OnImportsSatisfied()
    {
        Dispatcher.Invoke(new Action(() => {
            DataGrid.ItemsSource = CustomerRepository.GetAllCustomers();
        }));
    }
}
```

When you have more imports in your exported part, you can recompose a subset of them by setting AllowRecomposition to true only for the relevant imports. As a subset for the initial composition, the OnImportSatisfied method of IPartImportSatisfiedNotification will be fired every time a recomposition occurs. In the previous sample, this notification causes the data grid to be refreshed.

When you prepare your application to have this dynamic behavior, you must be aware of the following facts:

- When recomposition occurs, imported properties and fields are replaced. For arrays and collections, that means, instead of updating the existing array or collection, it is replaced with a new array or collection instance.
- Recomposition is not supported with the ImportingConstructor pattern.

As a best practice, it is worth designing your exported parts with recomposition in mind, even if you do not allow this. It will adorn your application with flexibility.

## Part lifetime

Once an application ships, the authors of that application won't have control over the set of parts. After deployment, third-party extensions can also play in. So, it's very important that you understand a part's lifetime, and its implications.

MEF parts are living in a composition container. This container is the owner entity of these parts, and is responsible for instantiating and disposing of them. This control is never transferred to any actor requesting the part from the container, or working with it indirectly (through an import). Both developers of exported parts, and consumers of importing that specific part, should be able to control the part's lifecycle by means of "shareability". When an exported part is shared, at most, one instance of that part may exist per container. If an export is non-shared, each request for that specific part is served by a new instance.

Exported parts can control their shareability with the PartCreationPolicy attribute that takes an argument with the type of CreationPolicy, as shown in the following example:

```csharp
[PartCreationPolicy(CreationPolicy.NonShared)]
[Export(typeof(IGreetings))]
public class MyNonSharedGreeting: IGreetings{
    // ...
}
```

The CreationPolicy enumeration has three values. Shared and NonShared have the meaning discussed earlier, and Any means the part author allows the part to be used as either Shared or NonShared. The attribute in the sample declares that every request for the MyNonSharedGreeting part should retrieve a new instance of part.

Imports can also constrain the creation policy of parts used to import the values. The Import and ImportMany have a property called RequiredCreationPolicy, and you can specify its value from the CreationPolicy enumeration type, as shown in the following example:

```csharp
[Export]
class Program {
    [ImportMany(RequiredCreationPolicy = CreationPolicy.NonShared)]
    private IEnumerable<IGreetings> Greetings { get; set; }
}
```

The behavior of the container is determined by the part creation policies of the export and the related imports. 10-10 summarizes this behavior.

## TABLE 10: Part Creation Behavior

| IMPORT BEHAVIOR | PART: ANY | PART: SHARED | PART: NONSHARED |
| --- | --- | --- | --- |
| Any | Shared | Shared | Non-shared |
| Shared | Shared | Shared | No match |
| NonShared | Non-shared | No match | Non-shared |

When any of the import and export part creation policies are set to Shared while the other is set to NonShared, the composition container does not make a match between the exported part and the import.

The composition container that is responsible for creating parts holds references for shared parts and for all non-shared parts that implement IDisposable, or are used in an import configured to allow recomposition. When the container is disposed, all references to parts held the container will be cleaned up. For parts implementing IDisposable, the Dispose method is called.

Non-shared parts that do not have references in the container are not disposed together with the container. Continuously requesting non-shared parts from the container may lead to memory issues, you must use them very carefully.

## Accessing Metadata

You can decorate exports with metadata attributes holding additional custom properties about the part. This metadata is used by the composition container for filtering — to decide whether an import matches the export or not. You can also access this metadata and utilize it in the program control logic.

Let's assume you develop parts implementing the ILoggerTask:

```csharp
interface ILoggerTask
{
    void WriteLog(LogItemType type, object message);
}
```

You want to be able to filter parts by the log entry item type they accept, and you also to know if they support transactional behavior or not. You would also like to assign names to the parts for diagnostic purposes. When these exports are ready, they could look like these sample classes:

```csharp
[LogChannelExport(ItemType = LogItemType.Error, IsTransactional = false)]
[ExportMetadata("Name", "Local Exports")]
public class LocalExportsChannel : ILoggerTask
{
    public void WriteLog(LogItemType type, object message) { /* ... */ }
}

[LogChannelExport(ItemType = LogItemType.All, IsTransactional = true)]
[ExportMetadata("Name", "All Log Messages")]
public class GeneralChannel : ILoggerTask
{
    public void WriteLog(LogItemType type, object message) { /* ... */ }
}

[Export(typeof(ILoggerTask))]
[ExportMetadata("Name", "Simple Channel")]
public class SimpleChannel : ILoggerTask
{
    public void WriteLog(LogItemType type, object message) { /* ... */ }
}
```

The export defines both weakly typed metadata specified with ExportMetadata attribute and strongly typed metadata defined by LogExport attribute:

```csharp
[MetadataAttribute]
[AttributeUsage(AttributeTargets.Class, AllowMultiple = false)]
public class LogExportAttribute : ExportAttribute
{
    public LogExportAttribute() : base(typeof(ILoggerTask)) { }
    public bool IsTransactional { get; set; }
    public LogItemType ItemType { get; set; }
}
```

You can access the metadata of your works in a weakly typed fashion with the following pattern:

```csharp
[ImportMany]
public Lazy<ILoggerTask, IDictionary<string, object>> AllChannelsWithMetadata { get; set; }
```

The second generic argument of the Lazy<,> type allows you to access the part metadata through the Metadata collection:

```csharp
foreach (var item in AllChannelsWithMetadata)
{
    Console.WriteLine("{0} {1}", item.Metadata["Name"],
    item.Metadata.ContainsKey("ItemType") ? item.Metadata["ItemType"] : "<none>");
}
```

When you intend to access the metadata in a strongly typed fashion, or you want to use it for implicit filtering, you must use a separate approach. Define a metadata view interface for read-only properties with your metadata property names, as shown in the following example:

```csharp
public interface ILogChannelProperties
{
    LogItemType ItemType { get; }
    [DefaultValue(false)]
    string Name { get; }
    [DefaultValue(false)]
    bool IsTransactional { get; }
}
```

As you can see, this metadata view contains all properties. While ItemType and IsTransactional were assigned to the exported part in a strongly typed manner, Name was used in a weakly typed way. In the Import definitions, use the following pattern:

```csharp
[ImportMany]
public Lazy<ILoggerTask, ILogChannelProperties[]> Channels { get; set; }
```

The second type argument of the Lazy<,> type provides access to the metadata through view properties:

```csharp
foreach (var item in Channels)
{
    Console.WriteLine("{0} {1}", item.Metadata.Name, item.Metadata.ItemType);
}
```
