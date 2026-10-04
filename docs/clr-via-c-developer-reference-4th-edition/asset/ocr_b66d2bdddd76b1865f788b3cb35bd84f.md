![](bbox=[0.125, 0.057, 0.672, 0.413])

**FIGURE 23-1** Hierarchy of the reflection types that encapsulate information about a type's member.

The following program demonstrates how to query type's members and display some information about them. This code processes all of the public types defined in all assemblies loaded in the calling AppDomain. For each type, the DeclaredMembers property is called and returns a collection of MemberInfo-derived objects; each object refers to a member defined within the type. Then, for each member, its kind (field, constructor, method, property, etc.) and its string value (obtained by calling ToString()) is shown.

```
using System;
using System.Reflection;

public static class Program {
    public static void Main() {
        // Loop through all assemblies loaded in this AppDomain
        Assembly[] assemblies = AppDomain.CurrentDomain.GetAssemblies();
        foreach (Assembly a in assemblies) {
            Show(0, "Assembly: {0}", a);
        }

        // Find Types in the assembly
        foreach (Type t in a.ExportedTypes) {
            Show(1, "Type: {0}", t);
        }

        // Discover the type's members
        foreach (MemberInfo mi in t.GetType().DeclaredMembers) {
            String typename = String.Empty;
            if (mi is Type) typename = "Nested Type";
            if (mi is FieldInfo) typename = "FieldInfo";
            if (mi is MethodInfo) typename = "MethodInfo";
            if (mi is ConstructorInfo) typename = "ConstructInfo";
        }
    }
}
```