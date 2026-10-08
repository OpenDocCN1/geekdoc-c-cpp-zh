# TABLE 20.2 Global Attributes

| Attribute | Purpose |
| --- | --- |
| **Informational Attributes** |  |
| AssemblyProduct | Specifies a product name for the assembly |
| AssemblyTrademark | Specifies a trademark for the assembly |
| AssemblyInformationalVersion | Specifies an information version for the assembly |
|  | Specifies a company name for the assembly |
| AssemblyCopyright | Specifies a copyright for the assembly |
| AssemblyFileVersion | Specifies a version number for the Windows file version resource |
| CLSCompliant | Indicates if the assembly is CLS-compliant |
| **Assembly Manifest Attributes** |  |
| AssemblyTitle | Specifies a title for the assembly manifest |
| AssemblyDescription | Specifies a description for the assembly manifest |
| AssemblyConfiguration | Specifies the configuration for the assembly manifest |
| AssemblyDefaultAlias | Specifies a friendly default alias for the assembly manifest |

# # Using Custom Attributes

If you need to provide custom metadata for your own applications, you can create custom attributes by defining an attribute class that derives from **Attribute**, either directly or indirectly.

For example, you can define a custom attribute that contains the Team Foundation Server Work Item number associated with a code change, as shown in Listing 20.7.

# LISTING 20.7 Creating a Custom Attribute

```
[AttributeUsage(AttributeTargets.All, Inherited = false, AllowMultiple = true)]
public sealed class WorkItemAttribute : System.Attribute
{
private int workItemId;
public WorkItemAttribute(int workItemId)
{
this.workItemId = workItemId;
}
```