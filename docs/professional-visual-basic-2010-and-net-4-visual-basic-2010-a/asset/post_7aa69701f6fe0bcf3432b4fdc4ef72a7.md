
The preceding list of referenced libraries is for .NET 4, so if you instead create a project that targets .NET 2.0, this list will be shorter. Keep in mind that changing your target framework does not update any existing references. If you are going to attempt to target the .NET 2.0 Framework, then you’ll want to remove references that have a version higher than 2.0.0.0. References such as System.Core enable new features in the System namespace that are associated with .NET 3.5.

To review details about the imported and referenced namespaces, select the References tab in your project properties display, as shown in Figure 1-10. This tab enables you to check for unused references and even define reference paths. More important, it is from this tab that you select other .NET Class Libraries and applications, as well as COM components. Selecting the Add drop-down button gives you the option to add a reference to a local DLL or a Web service.

![](img/d99870e80390742f93963da7be0b2e61_43_0.png)

## FIGURE 1-10

When referencing DLLs you have three options: Reference an assembly from the GAC, reference an assembly based on a file path, or reference another assembly from within your current solution. Each of these options has advantages and disadvantages. The only challenge for assemblies that are in the GAC is that your application is dependent on what is potentially a shared resource. In general, however, for assemblies that are already in the GAC, referencing them is a straightforward, easily maintainable process.

In addition to referencing libraries, you can reference other assemblies that are part of your solution. If your solution consists of more than a single project, then it is straightforward and highly recommended to use project references in order to enable those projects to reference each other. While you should avoid circular references — Project A references Project B which references Project A — using project references is preferred over file references. With project references, Visual Studio can map updates to these assemblies as they occur during a build of the solution. It’s possible for Visual Studio to automatically update the referenced assemblies in your executable project to be the latest build of the referenced DLLs that are part of the same solution. Note that the target needs to be an executable. Visual Studio will automatically update references between DLL projects in a common solution.

This is different from adding a reference to a DLL that is located within a specified directory. When you create a reference via a path specification, Visual Studio can check that path for an updated copy of the reference, but your code is no longer as portable as it would be with a project reference. More important, unless there is a major revision, Visual Studio usually fails to detect the types of changes you are likely to make to that file during the development process. As a result, you’ll need to manually update the referenced file in the local directory of the assembly that’s referencing it. For your own code often it’s best to leverage project references, rather than path-based references. However, for third party controls where you’ll often only have an installed location, one which isn’t likely to change as you move between machines, a path based reference can work.

On the other hand an alternative solution which is commonly used, is to ensure that instead of referencing third party controls based on their location, that instead ‘copy local’ references are used so that the version specific copy of the control deploys with the code that depends on it. This means that different versions of the controls can exist on the same server in different applications. Additionally because a local copy of the control is with the application, the application can be XCOPY deployed without needing to register the controls.

## Resources

In addition to referencing other assemblies, it is quite common for a .NET application to need to reference things such as images, icons, audio, and other files. These files aren’t used to provide application logic but are used at runtime to provide support for the look, feel, and even text used to communicate with the application’s user. In theory, you can reference a series of images associated with your application by looking for those images based on the installed file path of your application. Doing so, however, places your application’s runtime behavior at risk, because a user might choose to replace, copy for profit, or just delete your files.

This is where project references become useful. Instead of placing the raw files onto the operating system alongside your executable, Visual Studio will package these files into your executable so that they are less likely to be lost or damaged. Figure 1-11 shows the Resources tab, which enables you to review and edit all the existing resources within a project, as well as import files for use as resources in your project. It even allows you to create new resources from scratch.

![](img/d99870e80390742f93963da7be0b2e61_44_0.png)

FIGURE 1-11

Note one little-known feature of this tab: Using the Add Resource drop-down button and selecting an image (not an existing image but one based on one of the available image types) will create a new image file and automatically open Microsoft Paint (for Express Edition developers); this enables you to actually create the image that will be in the image file.

Users of Visual Studio 2010 have additional capabilities not supported by Visual Basic’s Express Edition. For one thing, instead of using Paint, Visual Studio provides a basic image-editing tool, so when Visual Studio developers add a new image (not from a file), this editor opens within Visual Studio.

Additionally, within the list of Add Resource items, Visual Studio users can select or create a new icon. Choosing to create a new icon opens Visual Studio’s icon editor, which provides a basic set of tools for creating custom icons to use as part of your application. This makes working with .ico files easier because you don’t have to hunt for or purchase such files online; instead, you can create your own icons.

However, images aren’t the only resources that you can embed with your executable. Resources also apply to the fixed text strings that your application uses. By default, people tend to embed this text directly into the source code so that it is easily accessible to the developer. Unfortunately, this leaves the application difficult to localize for use with a second language. The solution is to group all of those text strings together, thereby creating a resource file containing all of the text strings, which is still part of and easily accessible to the application source code. When the application is converted for use in another language, this list of strings can be converted, making the process of localization easier. Localization is covered in detail in Chapter 27.

> The next tab is the Services tab. This tab is discussed in more detail in Chapter 13, which addresses services.

## Settings

As noted earlier in the discussion of the Solution Explorer, the default project template does not create any application settings; accordingly, an app.config file is neither needed nor created. app.config files are XML files that define any custom application settings that a developer wants to be able to change without needing to recompile the application. Because these settings live in an XML file, they can be modified in between or even during application execution.

One original goal of .NET was to reduce the version conflict that can occur when a component has registered with global settings. A conflict would occur if two different applications were attempting to reference two different versions of that component. Because the settings were global and stored in the central system registry, only one could be registered correctly. Since the different applications each wanted its specific version of the component and related settings, one of the applications worked while the other application broke.

.NET provided the capability to place version-specific project references in a local directory with the application, enabling two different applications to reference the appropriate version of that component. However, the second part of the problem was the central application settings. The app.config file provides the same capability, but its goal is to allow for local storage of application settings. Under .NET 1.x, support for application settings was still minimal, as most developers were still looking to the central system registry for this purpose. At the same time, the developer tools associated with settings were also minimal.

Fortunately, under .NET 2.0 this changed dramatically. Visual Studio 2010 provides significant support for application settings, including the Settings tab, shown in Figure 1-12. This tab enables Visual Basic developers to identify application settings and automatically create these settings within the app.config file.
