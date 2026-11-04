
This at the level of API structuring is reducing one level of clutter, while we're still faced with a challenge of finding interfaces and auxiliary types that typically live in one single flat namespace:

```
HRESULT hr;

// The following interface is declared in a flat namespace.
IBackgroundCopyJob* pJob = ...;

hr = pJob->AddFile(L"http://foo/bar.txt", L"c:\\temp\\bar.txt");
if (SUCCEEDED(hr))
{
    ...
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1244_0.png)

FIGURE 24.1 Win32 functions live in a flat namespace.

Figure 24.2 shows the use of a COM API, where this time all interfaces get lumped together in a flat declaration space, often improving on the situation a little bit by using some prefix scheme for interface names.

Furthermore, now that we've introduced some level of typing in APIs, we get a “nice” mix of top-level functions, interfaces, enums, and so on (all lumped together). This is similar to having folders in a file system but sticking a whole bunch of files in the root folder anyway.

Also notice the somewhat-related problems (elaborated on during our discussion of assemblies in Chapter 25, “Assemblies, and Application Domains”) of versioning, creating cryptic type names with integer suffixes or Win32 functions with an Ex suffix (for extended).

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1245_0.png)

FIGURE 24.2 COM interfaces push the declaration space problem one level up.

## HEADER NIGHTMARES

The use of headers in C and C++ is a notorious source of headaches. Various reasons come to mind, including the problems with duplicate definitions (requiring use of preprocessor tricks), the order of inclusion, and the separate notion of lib files that have to be linked in for things to work.

In the world of .NET, assemblies are self-describing and also act as the means to refer to a library during development time. Although reference assemblies are dehydrated from a code perspective (hence they're somewhat like very rich headers, including type and member information), they don't suffer from the problems related to headers.

It's clear that the approaches taken by the C-influenced world of Win32, COM, and so on have various drawbacks, such as the following:

- Discoverability of APIs is quite painful because all functions and types live in a single flat namespace (which can also lead to name clashes).
- Tooling can't help much with finding APIs, and providing decent IntelliSense support is challenging.
- Building applications requires multiple references to libraries, including the use of headers and a link-time reference to a library file.

## Assemblies and Namespaces

Because several of the previously mentioned problems are related, it's good to take a look at them collectively. One central issue has to do with tooling, where the requirement of headers describing binary libraries can be solved by bundling this metadata with the code of the library. This is precisely what assemblies do, as shown in Figure 24.3.

```
using Contoso.CashFlow.Client;

class Program
{
    static void Main()
    {
        var t = new Terminal();
    }
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1247_0.png)

FIGURE 24.4 Namespaces are merely an illusion created by front-end languages.

On the first line of this C# fragment, we're importing the namespace, such that we can simply write Terminal rather than the long type name (including the namespace). At the IL level, though, the full type name is used.

In front of the fully qualified type name Contoso.CashFlow.Client.Terminal, another name is specified in between brackets. This corresponds to the name of the assembly defining the type. Here we've compiled the Terminal type into an assembly with the name ContosoCFCClient. For the CLR to know where to find the type being referred to, it needs to know what assembly to look in.

This brings us to a discussion about the difference between namespaces and assemblies. In short, the two are mostly unrelated concepts. The name of an assembly doesn't dictate what namespaces can be defined inside it, nor does the name of a type (and its namespace) pose restrictions on which assembly it can be defined in. The only real relationship between both concepts is the fact that assemblies contain types and types live in namespaces, and therefore assemblies contain namespaces. In fact, the definition of a namespace can be spread across multiple assemblies, as exemplified by the framework assemblies System.dll (which, for instance, contains the System.Uri class) and mscorlib.dll (containing types like System.String).

## MSCORLIB VERSUS SYSTEM

Why are there multiple assemblies defining types of the Framework's top-level System namespace? The answer is partly historical and partly technical.

One of the more technical arguments is that mscorlib.dll has quite a few types that aren't just managed but make so-called internal calls into functionality that's defined at the CLR level. A good example of such a type is System.Object, which has many runtime representations and relies on CLR code for some of its core operations (such as GetType, which talks to metadata services).

When building applications in languages like C#, mscorlib will always be included by default, and so will System.dll. You can easily get rid of the latter if you really want to for some obscure reason, by dropping it from the referenced assembly list in Visual Studio's Solution Explorer. To exclude mscorlib.dll, you must dig a little deeper in the Project properties, under Build, Advanced.

## Declaring Namespaces

To declare a new namespace, use the namespace keyword in C#:

```
namespace Contoso.CashFlow.Client
{
    // Classes, structs, interfaces, enums, delegates, etc. can go in here
}
```

The default namespace chosen for new code files in a Visual Studio project is based on a setting specified for the project. This setting, shown in Figure 24.5, gets its default value from the name of the project upon creation. The output assembly name follows this default inferred value, too. It's considered good practice to reflect the top-level namespace for types defined in an assembly in the assembly's name. For example, the System.Web assembly (mostly) contains System.Web functionality.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1248_0.png)

FIGURE 24.5 Default namespace configuration setting.

Namespaces can be nested in a variety of ways. One is using the dot-separated notation for namespace names, which really establishes a hierarchy of nested namespaces. As an alternative, you can physically nest namespace declarations in one another:

```
namespace Contoso
{
    namespace CashFlow
    {
        namespace Client
        {
            // Types could go here...
            // ...as well as other subnamespaces
        }

        // More types could go here...
        // ...as well as namespaces that are siblings to Client
    }

    // And so on...
}
```

The dot notation is usually preferred because it avoids large indentation levels in code files, and it is better to avoid declaring multiple sibling namespaces in the same file.

It's advisable to reflect the namespace and type structure in the project's directory name and filename structure. The root folder of the project corresponds to the top-level namespace, subfolders to nested namespaces, and files to type names.

Visual Studio will infer the namespace for a new code file based on the folder in which it's located, as shown in Figure 24.6. The namespace name can always be changed in the code itself, but following this folder and file pattern is usually beneficial in terms of finding declarations quickly (especially if you're doing so outside the IDE without the aid of tools such as Class View or Object Explorer).

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1249_0.png)

FIGURE 24.6 Visual Studio reflects folder structure in namespace names.

From a runtime and language compiler point of view, the physical location of a code file doesn't have any impact whatsoever. All that matters is what the code says about namespace and type names. What the runtime sees are types with unique names within an assembly.
