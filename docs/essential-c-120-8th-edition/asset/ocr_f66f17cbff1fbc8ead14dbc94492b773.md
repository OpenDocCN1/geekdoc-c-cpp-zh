# Namespaces

Namespaces are a categorization mechanism for grouping all types related to a particular area of functionality. Namespaces are hierarchical and can have arbitrarily many levels in the hierarchy, though namespaces with more than half a dozen levels are rare. Typically, the hierarchy begins with a company name, and then a product name, and then the functional area. For example, in Microsoft.Win32.Networking, the outermost namespace is Microsoft, which contains an inner namespace Win32, which in turn contains an even deeply nested namespace.

Namespaces are primarily used to organize types by functionality so that they can be more easily found and understood. However, they can also be used to avoid type name collisions. For example, the compiler can distinguish between two types with the name Button as long as each has a different namespace. Thus you can disambiguate types System.Web.UI.WebControls.Button and System.Windows.Controls.Button.

In Listing 5.2, the Console type is found within the System namespace. The System namespace contains the types that enable the programmer to perform many fundamental programming activities. Almost all C# programs use types within the System namespace. Table 5.1 provides a listing of other common namespaces.

# TABLE 5.1: Common Namespaces

| Namespace | Description |
| --- | --- |
| System | Contains the fundamental types and types for conversion between types, mathematics, program invocation, and environment management. |
| System.Collections.Generics | Contains strongly typed collections that use generics. |
| System.Data.Entity | A framework designed to store and retrieve data from a relational database through code generation that maps entities into tables. |
| System.Drawing | Contains types for drawing to the display device and working with images. Note, however, it is most Windows specific. |