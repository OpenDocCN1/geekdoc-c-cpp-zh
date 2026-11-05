```
```
CodeContracts: CodeContractsDemo: Inferred 0 object invariants
CodeContracts: CodeContractsDemo: Retained 0 object invariants after filtering
CodeContracts: CodeContractsDemo: Discovered 3 postconditions to suggest
CodeContracts: CodeContractsDemo: Retained 1 postconditions after filtering
CodeContracts: CodeContractsDemo: Detected 1 code fixes
CodeContracts: CodeContractsDemo: Proof obligations with a code fix: 3
C:\\Program Files (x86)\\Microsoft Visual Studio 14.0\\Common7\\IDE\\CodeContractsDemo.exe(1,1): message : CodeContracts:
Checked 15 assertions: 13 correct (2 masked)
CodeContracts: CodeContractsDemo:
CodeContracts: CodeContractsDemo: Static contract analysis done.
========== Rebuild All: 1 succeeded, 0 failed, 0 skipped ==========
```
```

*Code Listing 57: Successful Build*

The problem here is that simply adding the [Pure] attribute to the CalculatedCutFactor method does not make it pure. This is the point I am trying to make with this section on method purity. We need to ensure that methods called inside a contract are pure because they are so by design, not because we have decorated them with the [Pure] attribute. Let's have a look at our CalculatedCutFactor method again and modify it slightly so that we are not violating the rules specified for method purity.

```
```csharp
public class DemoPurity
{
    /// <summary>
    /// Property for cutting factor
    /// </summary>
    public int CutFactor { get; private set; }

    /// <summary>
    /// Public Constructor
    /// </summary>
    /// <param name="cutFactor"></param>
    public DemoPurity(int cutFactor)
    {
        CutFactor = cutFactor;
    }

    /// <summary>
    /// Calculate the volume cut
    /// </summary>
    /// <param name="volumeSteel"></param>
    /// <param name="factorModifier"></param>
    /// <returns></returns>
    public int VolumeCut(int volumeSteel, int factorModifier)
    {
```
```