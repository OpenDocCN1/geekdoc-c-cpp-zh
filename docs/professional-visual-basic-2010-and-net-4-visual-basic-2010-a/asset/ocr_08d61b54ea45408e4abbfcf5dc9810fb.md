The main purpose of the configuration file is to provide binding-related information to the developer or administrator who wishes to override the default policy handling of the CLR.

Specifically, the configuration file, as it’s written in XML, has a root node named <configuration>, and it must have the end node of </configuration> present to be syntactically correct. The configuration file is divided into specific types of nodes that represent different areas of control. These areas are as follows:

+   - Startup
+   - Runtime
+   - Remoting
+   - Crypto
+   - Class API
+   - Security

Although all of these areas are important, this chapter covers only the first two. All of the settings discussed can be added to the application configuration file. Some of the settings (these are pointed out) can also be added to the machine configuration file. If a setting in the application configuration file conflicts with one in the machine configuration file, then the setting in the machine configuration file is used. When we talk about assembly references in the following discussion of configuration settings, we are talking exclusively about shared assemblies (which implies that the assemblies have a strong name, as required by assemblies in the GAC).

# Startup Settings

The <startup> node of the application and machine configuration files has a <requiredRuntime> node that specifies the runtime version required by the application. This is because different versions of the CLR can run on a machine side by side. The following example shows how you would specify the version of the .NET runtime inside the configuration file:

```
<configuration>
  <startup>
    <requiredRuntime version ="4.0.xxxx" safemode ="true"/>
  </startup>
</configuration>
```

# Runtime Settings

The runtime node, which is written as <runtime> (not to be confused with <requiredRuntime>), specifies the settings that manage how the CLR handles garbage collection and versions of assemblies. With these settings, you can specify which version of an assembly the application requires, or redirect it to another version entirely.

# Loading a Particular Version of an Assembly

The application and machine configuration files can be used to ensure that a particular version of an assembly is loaded. You can indicate whether this version should be loaded all the time or should only replace a specific version of the assembly. This functionality is supported through the use of the <assemblyIdentity> and <bindingRedirect> elements in the configuration file, as shown in the following example:

```
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <dependentAssembly>
        <assemblyIdentity name="AssemblyName"
                          publickeytoken="b77a5c561934e089"
                          culture="en-us"/>
        <bindingRedirect oldVersion="*"
                         newVersion="2.0.50.0"/>
      </dependentAssembly>
    </assemblyBinding>
  </runtime>
</configuration>
```