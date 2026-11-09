Having discussed only the probing element's privatePath attribute in Chapter 2, I'm going to discuss the other XML configuration file elements in this section. Following is an XML configuration file.

```
```xml
<?xml version="1.0"?>
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <probing privatePath="AuxFiles;bin\subdir" />

      <dependentAssembly>

        <assemblyIdentity name="SomeClassLibrary"
          publicKeyToken="32ab4ba45e0a69a1" culture="neutral"/>

        <bindingRedirect
          oldVersion="1.0.0.0" newVersion="2.0.0.0" />

        <codeBase version="2.0.0.0"
          href="http://www.Wintellect.com/SomeClassLibrary.dll" />

      </dependentAssembly>

      <dependentAssembly>

        <assemblyIdentity name="TypeLib"
          publicKeyToken="1f2e74e897abbcfe" culture="neutral"/>

        <bindingRedirect
          oldVersion="3.0.0.0-3.5.0.0" newVersion="4.0.0.0" />

        <publisherPolicy apply="no" />

      </dependentAssembly>

    </assemblyBinding>
  </runtime>
</configuration>
```
```

This XML file gives a wealth of information to the CLR. Here's what it says:

+   - **probing element** Look in the application base directory's AuxFiles and bin\subdir directories when trying to find a weakly named assembly. For strongly named assemblies, the CLR looks in the GAC or in the URL specified by the codeBase element. The CLR looks in the application's private paths for a strongly named assembly only if no codeBase element is specified.
+   - **First dependentAssembly, assemblyIdentity, and bindingRedirect elements** When attempting to locate version 1.0.0.0 of the culture-neutral SomeClassLibrary assembly published by the organization that controls the 32ab4ba45e0a69a1 public key token, locate version 2.0.0.0 of the same assembly instead.
+   - **codeBase element** When attempting to locate version 2.0.0.0 of the culture-neutral SomeClassLibrary assembly published by the organization that controls the 32ab4ba45e0a69a1.