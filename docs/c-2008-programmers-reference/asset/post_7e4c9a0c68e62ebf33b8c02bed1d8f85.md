
## Part II: Application Development Using C#
### Chapter 18: Developing Windows Mobile Applications
### Creating a MSI File

You can now create the MSI installer to install the application onto the user’s computer and then invoke the custom installer built in the previous section to instruct the Windows CE Application Manager to install the application onto the device.

Using the same solution, add a new Setup Project (see Figure 18-38). Name the project `RSSReaderSetup`.

![](img/a977a875c7c627b45d939729705a252e_632_0.png)

Figure 18-38

Using the newly created project, you can now add the various components and files that you have been building in the past few sections. Right-click on the `RSSReaderSetup` project in Solution Explorer, and select Add → File (see Figure 18-39).

![](img/a977a875c7c627b45d939729705a252e_632_1.png)

Figure 18-39

Add the following files (see Figure 18-40):

- `SmartDeviceCab1\Release\RSSReader.CAB`
- `RSSReaderInstaller\bin\Release\RSSReaderInstaller.dll`
- `RSSReaderInstaller\setup.ini`

![](img/a977a875c7c627b45d939729705a252e_633_0.png)

These three files will be copied to the user's computer during the installation.

The next step is to configure the MSI installer to perform some custom actions during the installation stage. Right-click the `RSSReaderSetup` project in Solution Explorer, and select View → Custom Actions (see Figure 18-41).

![](img/a977a875c7c627b45d939729705a252e_633_1.png)

The Custom Actions tab displays. Right-click on Custom Actions, and select Add Custom Action (see Figure 18-42).

![](img/a977a875c7c627b45d939729705a252e_634_0.png)

Figure 18-42

Select Application Folder, select the `RSSReaderInstaller.dll` file (see Figure 18-43), and click OK.

![](img/a977a875c7c627b45d939729705a252e_634_1.png)

Figure 18-43

The Custom Actions tab should now look like Figure 18-44.

![](img/a977a875c7c627b45d939729705a252e_634_2.png)

Figure 18-44

Set the various properties of the `RSSReaderSetup` project as shown in the following table (see Figure 18-45).

| Property | Value |
|---|---|
| Author | Wei-Meng Lee |
| Manufacturer | Developer Learning Solutions |
| ProductName | RSSReader |

![](img/a977a875c7c627b45d939729705a252e_635_0.png)

Figure 18-45

The last step is to build the project. Right-click on the `RSSReaderSetup` project in Solution Explorer, and select Build.

The MSI installer is now in the `\Release` subfolder of the folder containing the `RSSReaderSetup` project (see Figure 18-46).

![](img/a977a875c7c627b45d939729705a252e_635_1.png)

Figure 18-46

### Testing the Setup

To test the MSI installer, ensure that your emulator (or real device) is connected to ActiveSync. Double-click the `RSSReaderSetup.msi` application, and the installation process begins (see Figure 18-47).

![](img/a977a875c7c627b45d939729705a252e_636_0.png)

Figure 18-47

Follow the instructions on the dialog. At the end, an Application Downloading Complete message displays (see Figure 18-48).

![](img/a977a875c7c627b45d939729705a252e_636_1.png)

Figure 18-48

Check your emulator (or real device) to verify that the application is successfully installed (see Figure 18-49).

![](img/a977a875c7c627b45d939729705a252e_637_0.png)

Figure 18-49

To uninstall the application, double-click the `RSSReaderSetup.msi` application again. This time, you see the dialog shown in Figure 18-50.

![](img/a977a875c7c627b45d939729705a252e_637_1.png)

Figure 18-50

If you choose to remove the application, the Windows CE Application Manager displays the list of programs that you have installed through ActiveSync (see Figure 18-51). To uninstall the RSS Reader application, uncheck the application and click OK. The application is removed.

![](img/a977a875c7c627b45d939729705a252e_638_0.png)

Figure 18-51

### Installing the Prerequisites — .NET Compact Framework 3.5

One problem you will likely face when deploying your application to real devices is that the target device does not have the required version of the .NET Compact Framework (version 3.5 is needed). Hence, you need to ensure that the user has a means to install the right version of the .NET Compact Framework. There are two ways of doing this:

- Distribute a copy of the .NET Compact Framework 3.5 Redistributable to your client. You can download a copy from http://microsoft.com/downloads. Users can install the .NET Compact Framework before or after installing your application. This is the easiest approach, but requires the user to perform the extra step of installing the .NET Compact Framework.
- Programmatically install the .NET Compact Framework during installation, using the custom installer. Earlier, you saw how you can invoke the Windows CE Application Manager from within the custom installer class by using the `.ini` file. In this case, you simply need to create another `.ini` file, this time to install the CAB file containing the .NET Compact Framework. The various CAB files for the .NET Compact Framework 3.5 can be found on your local drive in the following directory: `C:\Program Files\Microsoft.NET\SDK\CompactFramework\v3.5\WindowsCE`. Figure 18-52 shows the various CAB files for each processor type (ARM, MIPS, SH4, X86, and so on). To install the .NET Compact Framework 3.5 on Windows Mobile 6 Standard devices, you just need to add the `NETCFv35.wm.armv4i.cab` file to the `RSSReaderInstaller` project, together with its associated `.ini` file.

![](img/a977a875c7c627b45d939729705a252e_639_0.png)

Figure 18-52

### Summary

This chapter explored developing applications for the Windows Mobile 6 platform, using the .NET Compact Framework. Using that framework, you can leverage your familiarity with the .NET Framework to develop compelling mobile applications. The RSS application is an example of a useful application that you can use on a daily basis. The chapter also explained how to package an application into a CAB file and then into a MSI package so that you can distribute it to your users easily.

## Developing Silverlight Applications

Over the years, we have all seen the proliferation of web applications. In the early days, web sites consisted of sets of static HTML pages with nice graphics and lots of information. Then, server-side technologies like CGI, ASP, and JSP made web applications possible, and suddenly users could do a lot of things on the web, including buying products and making reservations online. Client-side innovations such as JavaScript helped improve the user experience of web applications, making them feel much more responsive. Although AJAX's underlying technologies had been available for several years, it wasn't really until the last couple of years that people really started spending more time AJAX-enabling their web applications. All this boils down to one important goal of web developers — making web applications much more interactive and responsive.

Today, a new term has been coined: RIA — Rich Internet Application. To Microsoft, RIA really stands for Rich Interactive Application. And it was with that in mind that Microsoft recently launched a new technology/product called Silverlight. Previously known as Windows Presentation Foundation/Everywhere (WPF/E), Microsoft Silverlight is a browser plug-in that enables developers to host RIAs that feature animation and vector graphics, as well as video playback.

This chapter will help you get started with Silverlight and provides an opportunity for you to get a feel for how Silverlight development works.

### The State of Silverlight

At the time of writing, there are two versions of Silverlight — 1.0 and 2 (previously known as version 1.1), the main difference being the support of .NET languages in version 2. For Silverlight version 1.0, you have to use JavaScript for writing your application logic. In version 2, in addition to JavaScript you can also use either C# or Visual Basic for your application logic, which is then executed by a version of the CLR built within the runtime.

> At the time of writing, Silverlight 2 is in Beta 1.
