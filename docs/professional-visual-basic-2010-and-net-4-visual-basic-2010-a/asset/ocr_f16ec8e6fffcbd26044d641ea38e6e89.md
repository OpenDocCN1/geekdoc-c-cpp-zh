Because there is a second namespace, System.Drawing, that has a child called Text, the compiler does not have a clear location for the Text namespace and, therefore, cannot resolve the StringBuilder class. The solution to this problem is to ensure that only a single version of the Text child namespace is found locally. That way, the compiler will use this namespace regardless of the global availability of the System.Drawing.Text namespace.

Imports statements specify to the compiler those namespaces that the code will use:

```
Imports Microsoft.Win32
Imports System
Imports SysDraw = System.Drawing
```

Once they are imported into the file, you are not required to fully qualify your object declarations in your code. For instance, if you imported the System.Data.SqlClient namespace into your file, then you would be able to create a SqlConnection object in the following manner:

```
Dim conn As New SqlConnection
```

Each of the preceding Imports statements illustrates a different facet of importing namespaces. The first namespace, Microsoft.Win32, is not imported at the global level. Looking at the reference list, you may not see the Microsoft assembly referenced directly. However, opening the Object Browser reveals that this namespace is actually included as part of the System.dll.

As noted earlier, the StringBuilder references become ambiguous because both System.Text and System.Drawing.Text are valid namespaces at the global level. As a result, the compiler has no way to determine which Text child namespace is being referenced. Without any clear indication, the compiler flags Text.StringBuilder declarations in the command handler. However, using the Imports System declaration in the module tells the compiler that before checking namespaces imported at the global level, it should attempt to match incomplete references at the module level. Because the System namespace is declared at this level, if System.Drawing is not, then there is no ambiguity regarding to which child namespace Text.StringBuilder belongs.

This sequence demonstrates how the compiler looks at each possible declaration:

+   - It first determines whether the item is a complete reference, such as System.Text.StringBuilder.
+   - If the declaration does not match a complete reference, then the compiler tries to determine whether the declaration is from a child namespace of one of the module-level imports.
+   - Finally, if a match is not found, then the compiler looks at the global-level imports to determine whether the declaration can be associated with a namespace imported for the entire assembly.

While the preceding logical progression of moving from a full declaration through module-level to global-level imports resolves the majority of issues, it does not handle all possibilities. Specifically, if you import System.Drawing at the module level, the namespace collision would return. This is where the third Imports statement becomes important — this Imports statement uses an alias.

# Aliasing Namespaces

Aliasing has two benefits in .NET. First, aliasing enables a long namespace such as System.EnterpriseServices to be replaced with a shorthand name such as COMPlus. Second, it adds a way to prevent ambiguity among child namespaces at the module level.

As noted earlier, the System and System.Drawing namespaces both contain a child namespace of Text. Because you will be using a number of classes from the System.Drawing namespace, it follows that this namespace should be imported into the form’s module. However, were this namespace imported along with the System namespace, the compiler would again find references to the Text child namespace ambiguous. By aliasing the System.Drawing namespace to SysDraw, the compiler knows that it should only check the System.Drawing namespace when a declaration begins with that alias. The result is that although multiple namespaces with the same child namespace are now available at the module level, the compiler knows that one (or more) of them should only be checked at this level when they are explicitly referenced.