Exported parts can control their shareability with the PartCreationPolicy attribute that takes an argument with the type of CreationPolicy, as shown in the following example:

```
[PartCreationPolicy(CreationPolicy.NonShared)]
[Export(typeof(IGreetings))]
public class MyNonSharedGreeting: IGreetings{
    // ...
}
```

The CreationPolicy enumeration has three values. Shared and NonShared have the meaning discussed earlier, and Any means the part author allows the part to be used as either Shared or NonShared. The attribute in the sample declares that every request for the MyNonSharedGreeting part should retrieve a new instance of part.

Imports can also constrain the creation policy of parts used to import the values. The Import and ImportMany have a property called RequiredCreationPolicy, and you can specify its value from the CreationPolicy enumeration type, as shown in the following example:

```
[Export]
class Program {
[ImportMany(RequiredCreationPolicy = CreationPolicy.NonShared)]
private IEnumerable<IGreetings> Greetings { get; set; }
```

The behavior of the container is determined by the part creation policies of the export and the related imports. 10-10 summarizes this behavior.

# TABLE 10: Part Creation Behavior

| IMPORT BEHAVIOR | PART: ANY | PART: SHARED | PART: NONSHARED |
| --- | --- | --- | --- |
| Any | Shared | Shared | Non-shared |
| Shared | Shared | Shared | No match |
| NonShared | Non-shared | No match | Non-shared |

When any of the import and export part creation policies are set to Shared while the other is set to NonShared, the composition container does not make a match between the exported part and the import.

The composition container that is responsible for creating parts holds references for shared parts and for all non-shared parts that implement IDisposable, or are used in an import configured to allow recomposition. When the container is disposed, all references to parts held the container will be cleaned up. For parts implementing IDisposable, the Dispose method is called.