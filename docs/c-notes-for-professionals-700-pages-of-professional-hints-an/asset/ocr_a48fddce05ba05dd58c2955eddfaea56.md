Less efficient but more general is as follows:

```
Type t = null;
foreach (Assembly ass in AppDomain.CurrentDomain.GetAssemblies())
{
    if (ass.FullName.StartsWith("System."))
        continue;
    t = ass.GetType(typeName);
    if (t != null)
        break;
}
```

Notice the check to exclude scanning System namespace assemblies to speed up the search. If your type may actually be a CLR type, you will have to delete these two lines.

If you happen to have the fully assembly-qualified type name including the assembly you can simply get it with

```
Type.GetType(fullyQualifiedName);
```

# Section 63.12: Determining generic arguments of instances of generic types

If you have an instance of a generic type but for some reason don't know the specific type, you might want to determine the generic arguments that were used to create this instance.

Let's say someone created an instance of List<T> like that and passes it to a method:

```
var myList = new List<int>();
ShowGenericArguments(myList);
```

where ShowGenericArguments has this signature:

```
public void ShowGenericArguments(object o)
```

so at compile time you don't have any idea what generic arguments have been used to create o. Reflection provides a lot of methods to inspect generic types. At first, we can determine if the type of o is a generic type at all:

```
public void ShowGenericArguments(object o)
{
    if (o == null) return;

    Type t = o.GetType();
    if (!t.IsGenericType) return;
    ...
```

Type.IsGenericType returns true if the type is a generic type and false if not.

But this is not all we want to know. List<> itself is a generic type, too. But we only want to examine instances of specific constructed generic types. A constructed generic type is for example a List<int> that has a specific type argument for all its generic parameters.

The Type class provides two more properties, IsConstructedGenericType and IsGenericTypeDefinition, to distinguish these constructed generic types from generic type definitions:

```
typeof(List<>).IsGenericType // true
typeof(List<>).IsGenericTypeDefinition // true
```