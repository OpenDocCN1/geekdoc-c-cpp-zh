The IFileCompression interface shown in Listing 8.1 is an example of an interface implementation. By convention—a convention so strong it is universal—the interface name is PascalCase with a capital “I” prefix.

# **LISTING 8.1: Defining an Interface**

```
```csharp
interface IFileCompression
{
    void Compress(string targetFileName, string[] fileList);
    void Uncompress(
        string compressedFileName, string expandDirectoryName);
}
```
```

IFileCompression defines the methods a type must implement to be used in the same manner as other compression-related classes. The power of interfaces is that they grant the ability to callers to switch among implementations without modifying the calling code.

One key characteristic of an interface is that it has no implementation and no data. Method declarations in an interface have a single semicolon in place of curly braces after the header. Fields (data) cannot appear in an interface declaration. When an interface requires the derived class to have certain data, it declares a property rather than a field. Since the property doesn’t contain any implementation as part of the interface declaration, it doesn’t reference a backing field.

The declared members of an interface describe the members that must be accessible on an implementing type. The purpose of nonpublic members is to make those members inaccessible to other code. Therefore, C# does not allow access modifiers on interface members; instead, it automatically defines them as public.

**Guidelines**
DO use PascalCasing and an “I” prefix for interface names.

# # Polymorphism through Interfaces

Consider another example, as shown in Listing 8.2: IListable defines the members that a class needs to support for the ConsoleListControl class to display it. As such, any class that implements IListable can use the