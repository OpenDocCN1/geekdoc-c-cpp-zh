You can have multiple groups within the &lt;properties&gt; tags, but you can have only one level of groups. This means that you can't nest a &lt;group&gt; element in another &lt;group&gt; or &lt;add&gt; element.

# Using Non-standard Data Types

In addition to the data types listed earlier as String, DateTime, and Int32, you can also use your own types (defined in the App_Code folder, for example).

As with the built-in .NET types, you need to refer to your type using its fully qualified name, which includes the namespace and the class name. Imagine that you have a type Preference that contains various properties (implemented as automatic properties in this example) related to the user's preference. To include this in the profile, you need to wrap it in a namespace first:

```
VB.NET
Namespace PlanetWrox
  Public Class Preference
    Public Property FavoriteColor As String
    Other properties go here
  End Class
End Namespace
```

```
C#
namespace PlanetWrox
{
  public class Preference
  {
    public string FavoriteColor { get; set; }
    // Other properties go here
  }
}
```

You then refer to the type in an &lt;add /&gt; element as follows:

```
<add name="Preferences" type="PlanetWrox.Preference" />
```

A situation where you might need to refer to a type in the profile setup is when you are using generics. Chapter 5 discusses how to refer to role names using a List of strings. Here's a quick refresh of the code you saw in that chapter:

```
VB.NET
Dim roles As New List (Of String)
...
roles.Add("Members")
```

```
C#
List<string> roles = new List<string>();
roles.Add("Members");
```

To give your profile a property that is of a Generic List type, you need to use some special syntax. The following setting in Web.config creates a property called FavoriteGenres that stores the user's favorite genres as a List (Of Integer) in VB.NET and as a List<int> in C#: