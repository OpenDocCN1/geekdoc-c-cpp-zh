```
</runtime>
</configuration>
```

The highlighted part in Listing 33.2 shows the values that you have entered while configuring your client to use the new version of the assembly.

In addition to the configuration file that is created using the .NET Framework 2.0 Configuration tool, we have two more types of configuration files; machine configuration and publisher policy. The machine configuration files are used to set system-wide information common to all the applications. These files reside in <WinDrive>:\Windows\Microsoft.NET\ Framework\v2.0.50727\CONFIG\, with the name machine.config.

Another type of configuration files are the publisher policy files. To understand their use, think of a situation where you want to redirect the clients, using a particular version of a shared assembly, to a new version of shared assembly. We can use the .NET Framework 2.0 Configuration tool and redirect the client to the new version of the shared assembly. However, imagine a situation when there are too many clients to configure; or even worse, you simply do not know how many clients are using the old version. In such a situation, you need to use the publisher policy files. Publisher policy files contain a system-wide policy, which ensures that all the applications that request a particular version of the assembly are redirected to a specified new version of the assembly. However, you need to store such a policy at a central location so that every client would be able to use it. We know that all the clients look into the GAC for shared assemblies; therefore, the publisher policy files can be placed in the GAC.

After a new version of an assembly is created and mentioned in the configurations files, the CLR attempts to find the assembly with the help of following two attributes:

+   - codebase
+   - probing

Let’s discuss about these attributes in detail.

# codebase

The codebase attribute is used to locate the assembly on a particular network instead of locating it in the local GAC. You can set the <codeBase> attribute in the application configuration file as shown in Listing 33.3:

# Listing 33.3: Showing the Code for Setting the Codebase Attribute

```
...
<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
  <dependentAssembly>
    <assemblyIdentity name="Sharedobject" publicKeyToken="deeb33795f7d292a"/>
    <codeBase version="2.0" href="file:///C:/NewGAC" />
  </dependentAssembly>
</assemblyBinding>
...
```

If your assembly is signed, you can specify any location on the Internet (in the form of URLs, such as http://localhost/shared.dll) or local network. However, for unsigned assemblies, the path specified must be relative to the application directory.

> NOTE
> If the codebase attribute is found in an application configuration file, the assembly is loaded at the runtime from the location specified in it. If the application fails to load the assembly from the location specified in the codebase attribute, the loading process is deemed to have failed.

# probing

Private assemblies are always located in the application directories (with a few exceptions where you have assemblies supporting different assembly cultures). If you need to place your assemblies in subfolders of the application folder, you can set up your application to look up the assembly in those subfolders by using the