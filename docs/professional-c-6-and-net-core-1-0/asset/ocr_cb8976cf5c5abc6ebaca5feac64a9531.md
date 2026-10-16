libraries that are not platform specific, you can use dependency injection. How to do this is part of the bigger sample in this chapter, which is covered in the “View Models” section.

# Sample Solution

The sample solution consists of a WPF and a Universal Windows Platform app for showing and editing a list of books. For this, the solution uses these projects:

+   - **BooksDesktopApp**—A WPF project for the UI of the desktop application with .NET Framework 4.6
+   - **BooksUniversalApp**—A UWP app project for the UI of a modern app
+   - **Framework**—A portable library containing classes that are useful for all XAML-based applications
+   - **ViewModels**—A portable library containing view models for both WPF and UWP
+   - **Services**—A portable library containing services used by the view models
+   - **Models**—A portable library containing shared models
+   - **Repositories**—A portable library that returns and updates items
+   - **Contracts**—A portable library for contract interfaces used with dependency injection

The portable libraries are configured with the targets .NET Framework 4.6 and Windows Universal 10.0.

Figure 31.8 shows the projects with their dependencies. The Framework and Contracts are needed from all other projects. Have a look at the ViewModels project; this will call the services, but it doesn’t have a dependency on the services—just the contracts that are implemented by the services.