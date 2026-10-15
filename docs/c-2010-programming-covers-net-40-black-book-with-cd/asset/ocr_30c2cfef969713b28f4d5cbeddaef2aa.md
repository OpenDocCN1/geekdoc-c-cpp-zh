3. Type 1.1.0.0 in the Requested Version field as this is the version the application is currently bound to and will request for.

4. Type file:///E:/NewGAC/SharedObject.dll in the URI field, as shown in Figure 33.20:

![](bbox=[0.27, 0.11, 0.67, 0.43])

Figure 33.20: Specifying Codebase Settings

5. Click the OK button.

6. Run the ASimpleClient application and it should run fine now.

# Configuring Codebase Settings Manually

You can apply the codebase setting to the configuration file (ASimpleClient.exe.config) of your application by adding the highlighted code, as shown in Listing 33.16:

Listing 33.16: Setting the Code of the ASimpleClient.exe.config File

```
<?xml version="1.0"?>
<configuration>
<runtime>
<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
<dependentAssembly>
<assemblyIdentity name="SharedObject" publicKeyToken="001fe4f7b2c7f625" />
<publisherPolicy apply="yes" />
<bindingRedirect oldversion="1.0.0.0" newversion="1.1.0.0" />
<codeBase version="1.1.0.0" href="file:///E:/NewGAC/SharedObject.dll" />
</dependentAssembly>
</assemblyBinding>
</runtime>
</configuration>
```

You can notice that the assemblyIdentity node specifies the public token to identify the assembly. However, note that the public token contains various numbers and alphabets, which can be entered incorrectly while entering it manually.

You can also add the codebase settings in your application to look up the older version of the assembly in E:\AnotherGAC by adding the second highlighted line in the configuration file, as shown in Listing 33.17:

Listing 33.17: Setting the Codebase Setting to Look for an Older Version of an Assembly

```
<?xml version="1.0"?>
<configuration>
<runtime>
<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
<dependentAssembly>
```