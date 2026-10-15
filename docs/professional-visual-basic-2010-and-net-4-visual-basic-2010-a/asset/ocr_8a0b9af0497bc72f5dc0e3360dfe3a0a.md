often referenced by their ProgID, but Visual Basic does not provide any support for appending the version number on the end of the ProgID.

For those of you who are unfamiliar with the term ProgID, it’s enough to understand that ProgIDs are developer-friendly strings used to identify a component. For example, Word.Application describes Microsoft Word. ProgIDs can be fully qualified with the targeted version of the component — for example, Word.Application.10 — but this is a limited capability and relies on both the application and whether the person using it chooses this optional addendum. As you’ll see in Chapter 7, a namespace is built on the basic elements of a ProgID, but provides a more robust naming system.

For many applications, .NET has removed the need to identify the version of each assembly in a central registry on a machine. However, some assemblies are installed once and used by multiple applications. .NET provides a global assembly cache (GAC), which is used to store assemblies that are intended for use by multiple applications. The CLR provides versioning support for all components loaded in the GAC.

The CLR provides two features for assemblies installed within the GAC:

+   Side-by-side versioning — Multiple versions of the same component can be simultaneously stored in the GAC.

+   Automatic Quick Fix Engineering (QFE) — Also known as hotfix support, if a new version of a component, which is still compatible with the old version, is available in the GAC, the CLR loads the updated component. The version number, which is maintained by the developer who created the referenced assembly, drives this behavior.

The assembly’s manifest contains the version numbers of referenced assemblies. The CLR uses the assembly’s manifest at runtime to locate a compatible version of each referenced assembly. The version number of an assembly takes the following form:

```
Major.Minor.Build.Revision
```

# Major.Minor.Build.Revision

Changes to the major and minor version numbers of the assembly indicate that the assembly is no longer compatible with the previous versions. The CLR will not use versions of the assembly that have a different major or minor number unless it is explicitly told to do so. For example, if an assembly was originally compiled against a referenced assembly with a version number of 3.4.1.9, then the CLR will not load an assembly stored in the GAC unless it has major and minor numbers of 3 and 4, respectively.

Incrementing the revision and build numbers indicates that the new version is still compatible with the previous version. If a new assembly that has an incremented revision or build number is loaded into the GAC, then the CLR can still load this assembly for applications that were compiled referencing a previous version.

# Better Deployment

Applications written using previous versions of Visual Basic and COM were often complicated to deploy. Components referenced by the application needed to be installed and registered (this information was stored in the registry); and for Visual Basic components, the correct version of the Visual Basic runtime needed to be available. The Component Deployment tool helped in the creation of complex installation packages, but applications could be easily broken if the dependent components were inadvertently replaced by incompatible versions on the client’s computer during the installation of an unrelated product.

In .NET, most components do not need to be registered. When an external assembly is referenced, the application decides between using a global copy (which must be in the GAC on the developer’s system) or copying a component locally. For most references, the external assemblies are referenced locally, which means they are carried in the application’s local directory structure. Using local copies of external assemblies enables the CLR to support the side-by-side execution of different versions of the same component. As noted earlier, to reference a globally registered assembly, that assembly must be located in the GAC. The GAC provides a versioning system that is robust enough to allow different versions of the