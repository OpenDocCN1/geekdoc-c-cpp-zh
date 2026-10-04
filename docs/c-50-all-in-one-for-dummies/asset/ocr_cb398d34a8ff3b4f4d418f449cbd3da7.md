# 512 Breaking Down the Projects

+   - Blank App: Just what it sounds like, a barebones Windows Store app.
- Grid and Split app: Two pretemplated sample apps for Windows Store that show off the listview.
- Class Library for Windows Store: Helps you build a .NET DLL.
- Windows Runtime Component: The templates to build WinMD components for Windows 8.
- Unit Test library for Windows Store: The add-on for unit testing in Windows 8.
- Windows Projects: Windows projects in Visual C are programs that compile into a running program, like Microsoft Word, or Visual Studio itself. The projects include
- Windows Forms Application: The classic "program." Compiles into a program that runs with its own window and with a red box (with the little X in it) to exit. This is the original Windows Program style, gradually replaced by Windows Presentation Foundation.
- Class Library: Makes a DLL when you're all done. This is the basis of the .NET Framework, and COM before. It is used to make blocks of reusable code.
- WPF Application: The new "program." Also compiles into an EXE, but uses a new user interface format called Windows Presentation Foundation. I cover this in depth in Book V.
- WPF Browser Application: Just like a WPF application but runs in Internet Explorer. This is not a Silverlight application; it's an XBAP application, for XML Browser Application. It has a smaller set of available user interface controls but still powerful.
- Console application: These EXEs are designed to run from a command prompt (or Windows Explorer).
- WPF Custom Library: This is a way to make actual custom controls that appear in the toolbox that you use in your WPF applications.
- Empty Project: Just what it sounds like — a project that's empty, poetic. It's used to build a program for you don't have a template.
- Windows Services: These programs appear in the Services panel. Didn't know you could make those with .NET? You aren't alone. It's a powerful feature that few people know about. Windows Services are essentially terminate-and-resident, or TSR, programs. (Remember those from your DOS days? They say in memory.)
- WPF User Control Library: The finished product of this looser control format doesn't appear in the toolbox but is much easier to build because it doesn't require coding the whole thing in C#.