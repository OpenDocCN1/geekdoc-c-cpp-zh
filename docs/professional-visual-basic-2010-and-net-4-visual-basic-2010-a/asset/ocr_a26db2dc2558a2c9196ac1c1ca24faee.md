In addition to the blog post, Jarod introduces a tool for generating the P/Invoke signatures. The P/Invoke Interop Assistant enables you to find existing P/Invoke interfaces and automatically generate the necessary Visual Basic code to call these interfaces from your .NET application. The P/Invoke Interop Assistant is available as a free download from MSDN at http://code.msdn.microsoft.com/WindowsAPICodePack.

# Windows API Code Pack

One more tool that is available to Visual Basic developers is the Windows API Code Pack for Microsoft .NET Framework. This is another free download from MSDN targeting operating system APIs, which aren’t directly available from within the .NET Framework. In this case the authors have chosen to create a library which provides .NET classes to wrap the associated P/Invoke calls.

The code pack provides a C# library which you can reference from your Visual Basic project. You can then make calls to take advantage of things like the Windows 7 taskbar via this library. The library ships with several additional examples demonstrating how to use the various library classes to access different capabilities with the OS. You can download the files from MSDN at http://code.msdn.microsoft.com/WindowsAPICodePack

# SUMMARY

Even with the migration to 64-bit environments, COM is not going to go away for quite some time, so .NET applications have to interoperate with COM, and they have to do it well. By the end of this chapter, you have achieved several things:

+   ► You made a .NET application early bind to a COM component, using the import features available in Visual Basic.
+   ► You looked at the underlying tool, TlbImp.
+   ► You managed to make the application late bind as well, although it wasn’t a pleasant experience.
+   ► You incorporated an ActiveX control into a .NET user interface, again using the features of Visual Basic.
+   ► You looked at using RegAsm and TlbExp to export type libraries from .NET assemblies in order to enable VB6 applications to use .NET assemblies as if they were COM components.
+   ► Additional interop capabilities provided by P/Invoke were introduced along with two freely available tools which allow you to leverage these capabilities.