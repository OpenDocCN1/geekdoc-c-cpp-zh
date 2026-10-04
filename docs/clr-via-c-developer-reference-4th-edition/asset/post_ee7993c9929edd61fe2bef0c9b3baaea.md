
AssemblyVersion This number is stored in the AssemblyDef manifest metadata. The CLR uses this version number when binding to strongly named assemblies (discussed in Chapter 3). This number is extremely important and is used to uniquely identify an assembly. When starting to develop an assembly, you should set the major, minor, build, and revision numbers and shouldn't change them until you're ready to work on the deployable version of your assembly. When Assembly-A references a strongly named Assembly-B, Assembly-B's version is embedded inside Assembly-A's AssemblyRef entry. This way, when the CLR needs to load Assembly-B, it knows exactly which version Assembly-A built and tested with. It is possible to have the CLR load a different version by using a binding redirect, which is discussed in Chapter 3.

# Culture

Version numbers, assemblies also have a culture as part of their identity. For example, I could have an assembly that is strictly for German, another for Swiss German, another for US English, and so on. Cultures are identified via a string that contains a primary and secondary tag (as described in RFC 1766). Table 2-6 shows some examples.

| Primary Tag | Secondary Tag | Culture |
| --- | --- | --- |
| De | (none) | German |
| De | AT | Austrian German |
| De | CH | Swiss German |
| En | (none) | English |
| En | GB | British English |
| En | US | US English |

In general, if you create an assembly that contains code, you don't assign a culture to it. This is because code doesn't use any culture-specific assumptions built into it. An assembly that isn't assigned a culture is referred to as *culture neutral*.

If you're designing an application that has some culture-specific resources to it, Microsoft highly recommends that you create one assembly that contains your code and your application's default (or fallback) resources. When building this assembly, don't specify a culture. This is the assembly that other assemblies will reference when they create and manipulate types it publicly.

Now you can create one or more separate assemblies that contain only culture-specific resources—no code at all. All assemblies that are marked with a culture are called *satellite assemblies*. For these satellite assemblies, assign a culture that accurately reflects the culture of the resources placed in the assembly. You should create one satellite assembly for each culture you intend to support.

You'll usually use the ALex tool to build a satellite assembly. You won't need a compiler because the satellite assembly should have no code contained within it. When using ALex, you specify the desired culture by using the /culture switch, where text is a string such as "en-US," representing US English. When you deploy a satellite assembly, you should place it in a subdirectory that matches the culture text. For example, if the application base directory is C:\MyApp the US English satellite assembly should be placed in the C:\MyApp-US subdirectory. At run time, you can access the satellite assembly's resources using the System.ResourceManager class.

![](img/0ce3b788d061e3d3095fa554b1a34adf_85_0.png)

Note It is possible to create a satellite assembly that contains code, though this practice is discouraged. If you prefer, you can specify the culture by using the System.Reflection.AssemblyCultureAttribute custom attribute instead of ALex's /culture switch, for example as shown here.

```
// Set assembly culture to Swiss German
[assembly:AssemblyCulture('de-CH')]
```

Normally, you won't build an assembly that references a satellite assembly. In other words, an assembly's AssemblyRef entries should all refer to culture-neutral assemblies. If you want to access types or members contained in a satellite assembly, you should use reflection techniques as discussed in Chapter 23, "Assembly Loading and Reflection".

# Simple Application Deployment (Privately Deployed Assemblies)

Throughout this chapter, I've explained how you build modules and how you combine those modules into an assembly. At this point, I'm ready to explain how to package and deploy all of the assemblies so that users can run the application.

Windows Store apps have strict rules about packaging assemblies, and Visual Studio will pack all of an application's required assemblies into a single .appx file, which is either uploaded to the Windows Store or be side-loaded onto a machine. When a user installs an .appx file, all the assemblies are placed in a directory where the CLR will load them and adds an application title to the user's Start screen. If other users install the same file, the previously installed assemblies are used and the new user gets a tile added to their Start screen. When a user uninstalls a Windows Store app, the system removes the tile from the Start screen. If no other users have installed the app, Windows deletes the directory along with all the assemblies. Note that different users can install different versions of the same Windows Store app. To accommodate this, Windows installs the assemblies into different directories so that multiple versions of a single app can reside on a single machine simultaneously.

For desktop (non-Windows Store) applications, assemblies don't dictate or require any special means of packaging. The easiest way to pack a set of assemblies is simply to copy all of the files directly. For example, you could put all of the assembly files on a CD-ROM and ship it to the user with a batch setup program that copies the files from the CD to a directory on the user's hard drive. Because the assemblies include all of the dependent assembly references and types, the user can run the application and the runtime will look for referenced assemblies in the application's directory. No modifications to the registry are necessary for the application to run. To uninstall it just delete all the files—that's.

> Note Using a batch file or some other simple "installation software" will get an application onto the user's machine; however, you'll need more sophisticated installation software to create shortcut links on the user's desktop and Start menu/screen. You can easily back and restore the application or move it from one machine to another, but the various shortcut links will require special handling.

Of, Visual Studio has a built-in mechanism that you can use to publish an application by deploying a project's Properties pages clicking the Publish tab. You can use the options available on the Publish tab using Visual Studio to produce an MSI file and copy the resulting MSI file to a website, FTP server, or site path. The MSI file can also install any prerequisite components such as the .NET Framework or Microsoft SQL Server Edition. Finally, the application can automatically check for updates and install them on the user's machine by taking advantage of ClickOnce technology.

Assemblies deployed to the same directory are called privately deployed assemblies because the files aren't shared with any other (unless the other application is deployed to the same directory). Privately deployed assemblies are a win for developers, and users, and administrators can simply be copied to an application's base directory, and the CLR will load and execute the code in them. In addition, an application can be uninstalled by simply deleting the assemblies in its directory. This allows simple back and restore as well.

This simple install/move/uninstall scenario is possible because each assembly has metadata indicating referenced assembly should be loaded; no registry settings are required. In addition, referencing referencing scopes every type. This means that an application always binds to the type it was built and tested with; the CLR can't load a different assembly that just happens to provide a type with the same name. This is different from COM, in which types are recorded in the registry, making them available to any application running on the machine.

In Chapter 3, I'll discuss how to deploy shared assemblies that are accessible by multiple applications.
