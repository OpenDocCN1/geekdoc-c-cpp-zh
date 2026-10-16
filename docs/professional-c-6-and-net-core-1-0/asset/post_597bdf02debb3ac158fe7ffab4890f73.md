
Entity Framework and each version’s new features.

| Entity Framework | Description |
|---|---|
| 1.0 | Available with .NET 3.5 SP1. This version offered a mapping through an XML file to map tables to objects. |
| 4.0 | With .NET 4, Entity Framework made a jump from version 1 to 4. |
| 4.1 | Code First Support. |
| 4.2 | Bug fixes. |
| 4.3 | Migrations added. |
| 5.0 | Released together with .NET 4.5 and offering performance improvements, supporting new SQL Server features. |
| 6.0 | Moved to a NuGet package. |
| 7.0 | A complete rewrite, also supporting NoSQL, running on Windows apps as well. |

Let’s get into some details. Entity Framework was originally released as part of the .NET Framework classes that come preinstalled with the .NET Framework. Entity Framework 1 was part of the first service pack of .NET 3.5, which was a feature update: .NET 3.5 Update 1.

The second version had so many new features that the decision was made to move to version 4 together with .NET 4. After that, Entity Framework was released at a faster cadence than the .NET Framework. To get a newer version of Entity Framework, a NuGet package had to be added to the application (versions 4.1, 4.2, 4.3). There was a problem with this approach. Classes that have already been delivered with the .NET Framework had to be used as is. Just additional features, such as Code First, have been added with NuGet packages.

With .NET 4.5, Entity Framework 5.0 was released. Again some of the classes come with the preinstalled .NET Framework, and additional features are part of NuGet packages. The NuGet package also made it possible to allow installing the NuGet package for Entity Framework 5.0 with .NET 4.0 applications. However, in reality the package decided (via a script) in a case when Entity Framework 5.0 is added to a .NET 4.0 project that the result would be Entity Framework 4.4 because some of the types required belong to .NET 4.5 and are not part of .NET 4.

The next version of Entity Framework solved this problem by moving all the Entity Framework types to a NuGet package; the types that come with the Framework itself are ignored. This allows using version 6.0 with older versions of the Framework; you aren’t restricted to 4.5. To not conflict with classes of the Framework, some types moved to a different namespace. Some features of ASP.NET Web Forms had an issue with that because original classes of the Entity Framework have been used, and these do not map that easily to the new classes.

During the different releases, Entity Framework gives different options for mapping the database tables to classes. The first two options were Database First and Model First. With both of these options, the mapping was done via XML files. The XML file is presented via a graphical designer, and it’s possible to drag entities from the toolbox to the designer for doing the mapping.

With version 4.1, mapping via code was added: Code First. Code First doesn’t mean that the database can’t exist beforehand. Both are possible: A database can be created dynamically, but also the database can exist before you write the code. Using Code First, you don’t do the mapping via XML files. Instead, attributes or a fluent API can define the mapping programmatically.

Entity Framework Core 1.0 is a complete redesign of Entity Framework, as is reflected with the new name. Code needs to be changed to migrate applications from older versions of Entity Framework to the new version. Older mapping variants, such as Database First and Model First, have been dropped, as Code First is a better alternative. The complete redesign was also done to support not only relational databases but also NoSQL. Azure Table Storage is one of the options where Entity Framework can now be used.

## Windows Desktop Applications

For creating Windows desktop applications, two technologies are available: Windows Forms and Windows Presentation Foundation. Windows Forms consists of classes that wrap native Windows controls; it’s based on pixel graphics. Windows Presentation Foundation (WPF) is the newer technology and is based on vector graphics.

WPF makes use of XAML in building applications. XAML stands for eXtensible Application Markup Language. This way to create applications within a Microsoft environment was introduced in 2006 and is part of the .NET Framework 3.0. .NET 4.5 introduced new features to WPF, such as ribbon controls and live shaping.

XAML is the XML declaration used to create a form that represents all the visual aspects and behaviors of the WPF application. Though you can work with a WPF application programmatically, WPF is a step in the direction of declarative programming, which the industry is moving to. Declarative programming means that instead of creating objects through programming in a compiled language such as C#, Visual Basic, or Java, you declare everything through XML-type programming. Chapter 29, “Core XAML,” introduces XAML (which is also used with XML Paper Specification, Windows Workflow Foundation, and Windows Communication Foundation). Chapter 30 covers XAML styles and resources. Chapter 34, “Windows Desktop Applications with WPF,” gives details on controls, layout, and data binding. Printing and creating documents is another important aspect of WPF that’s covered in Chapter 35, “Creating Documents with WPF.”

What’s the future of WPF? Isn’t the UWP the UI platform to use for new applications going forward? UWP has advantages in supporting mobile devices as well. As long as some of your users have not upgraded to Windows 10, you need to support older operating systems such as Windows 7. UWP apps don’t run on Windows 7 or Windows 8. You can use WPF. In case you also would like to support mobile devices, it’s best to do as much code sharing as possible. You can create apps with both WPF and UWP by using as much common code as possible by supporting the MVVM pattern. This pattern is covered in Chapter 31, “Patterns with XAML Apps.”

## Universal Windows Platform

The Universal Windows Platform (UWP) is a strategic platform from Microsoft. When you use the UWP to create Windows apps, you’re limited to Windows 10 and newer versions of Windows. But you’re not bound to the desktop version of Windows. With Windows 10 you have a lot of different options, such as Phone, Xbox, Surface Hub, HoloLens, and IoT. There’s one API that works on all these devices!

One API for all these devices? Yes! Each device family can add its own Software Development Kit (SDK) to add features that are not part of the API that’s available for all devices. Adding these SDKs does not break the application, but you need to programmatically check whether an API from such an SDK is available on the platform the app is running. Depending on how many API calls you need to differentiate, the code might grow into a mess; dependency injection might be a better option.

> NOTE Dependency injection is discussed in Chapter 31, along with other patterns useful with XAML-based applications.

You can decide what device families to support with your applications. Not all device families will be useful for every app.

Will there be newer versions of Windows after Windows 10? Windows 11 is not planned. With Windows apps (which are also known as Metro apps, Windows Store apps, Modern apps, and Universal Windows apps) you’ve targeted either Windows 8 or Windows 8.1. Windows 8 apps typically were also running on Windows 8.1, but not the other way around. Now this is very different. When you create an app for the Universal Windows Platform, you target a version such as 10.0.10130.0 and define what minimum version is available and what latest version was tested, and the assumption is that it runs on future versions as well. Depending on the features you can use for your app and what version you’re expecting the user to have, you can decide what minimum version to support. Personal users will typically automatically update to newer versions; Enterprise users might stick to older versions.
