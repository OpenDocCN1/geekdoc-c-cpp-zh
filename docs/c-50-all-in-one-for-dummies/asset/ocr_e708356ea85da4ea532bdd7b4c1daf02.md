# Hacking the Project Types

# Hacking Project templates

The first, most obvious target for hacking are the project types because they are text based and have a lot of useful information in. Found in the IDE folder referenced in the preceding paragraph, the ProjectTemplates folder follows the hierarchy of the New Project tree (see Figure 3-4).

![](bbox=[0.235, 0.243, 0.735, 0.532])

Figure 3-4:
A bunch of project-type directories.

I focus on the CSharp directory tree because this book is about C#. To keep examples to a minimum, open the Windows/1033 folder, in order to view Windows project types. In a default install, that looks something like:

+   * ClassLibrary
* ConsoleApplication
* EmptyProject
* PortableClassLibrary
* WindowsApplication
* WindowsControlLibrary
* WindowsService
* WPFApplication
* WPFBrowserApplication

Book IV
Chapter 3
Customizing Visual Studio