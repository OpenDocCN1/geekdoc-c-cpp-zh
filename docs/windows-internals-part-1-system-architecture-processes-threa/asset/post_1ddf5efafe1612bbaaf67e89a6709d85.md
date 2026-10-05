
# Windows API flavors

The Windows API originally consisted of C-style functions only. Today, thousands of such functions exist for developers to use. C was the natural choice at the time of the inception of Windows because it was the lowest common denominator (that is, it could be accessed from other languages as well) and low level enough to expose OS services. The downside is the sheer number of functions coupled with the lack of naming consistency and logical groupings (for example, C++ namespaces); one of these difficulties resulted in some APIs using a different API mechanism: the Component Object Model (COM).

COM was originally created to enable Microsoft Office applications to communicate and exchange data between documents (such as embedding an Excel chart inside a Word document or a PowerPoint presentation). This ability is called Object Linking and Embedding (OLE). OLE was originally using an old Windows messaging mechanism called Dynamic Data Exchange (DDE); DDE was inherently limited, which is why a new way of communication was developed: COM. From initially COM2, released to the public circa 1993.

COM is based on two fundamental principles. First, clients communicate with objects (sometimes COM server objects) through interfaces—well-defined contracts with a list of logically related methods grouped under the virtual table dispatch mechanism, which is also a common way for C++ compilers to implement virtual functions dispatch. This results in binary compatibility and removes compiler name mangling issues. Consequently, it is possible to call these methods from many languages (and compilers), such as C, Visual Basic, .NET languages, and others. The second principle is that component implementation is loaded dynamically rather than statically linked to the client.

> Note Examples of APIs accessed through COM include DirectShow, Windows Media Foundation, DirectX, DirectComposition, Windows Imaging Component (WIC), and the Background Intelligent Transfer Service (BITS).

# The Windows Runtime

Windows 8 introduced a new API and supporting runtime called Windows Runtime (sometimes abbreviated WinRT, not to be confused with Windows RT, the discontinued ARM-based Windows OS version). The Windows Runtime consists of platform services developed early at particular for the so-called Windows Apps (formerly known as Metro Apps, Modern Apps, Immersive Apps, and Windows Store Apps). Windows Apps may target multiple device forms, from small IoT devices to phones, tablets, laptops, desktops, and even devices such as the Xbox One and Microsoft HoloLens.

From an API perspective, WinRT is built on top of COM, adding extensions to the base COM infrastructure. For example, complete type metadata is available in WinRT (stored in WINMD files and based on the .NET metadata format) that extends a similar concept in COM known as type libraries. From an API design perspective, it's much more cohesive than classic Windows API functions, with namespaces hierarchies, consistent naming, and programmatic patterns.

Windows Apps are subject to new rules, unlike the normal Windows applications (now desktop applications or Classic Windows applications). These rules are described in Chapter 9, "Management mechanisms," in Part 2.

The relationship between the various APIs and applications is not straightforward. Desktop apps can use a subset of WinRT APIs. Conversely, Windows Apps can use a subset of Win32 and COM APIs. Refer to the MSDN documentation for the details of which APIs are available from each platform. Note, however, at the binary level, the WinRT API is still based on top of the legacy Windows binaries and APIs, even though the availability of certain APIs may not be documented or supported. It is not a new "native" API for the system, much like .NET leverages the Windows APIs.

Applications written in C++, C# (or other .NET languages), and JavaScript consume WinRT APIs easily thanks to language projections developed for them. For C++, Microsoft created a non-standard extension known as C++/CX which makes simpler to consume WinRT types. A normal COM interop layer for .NET (with some supporting run-time extensions) allows .NET to consume WinRT APIs naturally and simply just if it were pure. For JavaScript developers, an extension called WinJS was developed for accessing WinRT, although JavaScript developers must still use HTML to build their app's interface.

> Even though HTML can be used in Windows Apps, it's still a local client app and not a web application retrieved from a web server.

# .NET Framework

The .NET Framework is part of Windows. Table 1-2 shows the .NET Framework installed as part of a given Windows version. However, a later version of the .NET Framework can be installed on older OS versions.

**TABLE 1-2** Default .NET Framework installations on Windows

| Windows Version | .NET Framework Version |
| :--- | :--- |
| Windows 8 | 4.5 |
| Windows 8.1 | 4.5.1 |
| Windows 10 | 4.6 |
| Windows 10 version 1511 | 4.6.1 |
| Windows 10 version 1607 | 4.6.2 |

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_22_0.png)

The .NET Framework consists of two components:

- **The Common Language Runtime** This is the run-time engine for .NET and includes a Just In Time (JIT) compiler that translates Common Intermediate Language (CIL) instructions to the underlying hardware CPU machine language, a garbage collector, type verification, code access security, and more. It's implemented as a COM in-process server (DLL) and uses various facilities provided by the Windows API.

- **The .NET Framework Class Library (FCL)** This is a large collection of types that implement functionality typically needed by client and server applications, such as user interface services, networking, database access, and much more.

By offering these features and others, including new high-level languages (C# the .NET Framework improves developer productivity and safety. ![](img/ff0e6a9d867a3a6e9527eb1d946810fc_23_0.png)

# Services, functions, and routines

Several terms in Windows API can have different meanings. The following list describes what terms mean:

- **Windows functions** These are documented. Examples include CreateProcess, CreateFile, and GetMessage.

- **Native system services (or calls)** These are undocumented. For example, NtCreateProcess calls to create a new process.

- **Kernel functions (or routines)** These are internal. For example, ExAllocatePoolWithTag allocates memory from pools.

- **Windows services** These are started by the service control manager. For example, Task Scheduler runs. (Note that although the registry defines drivers as "services", they are not referred to as such.)

- **Dynamic link libraries (DLLs)** These are binary files. Examples include Msvcrt.dll (the C run-time library) and Kernel32.dll (one of the Windows subsystem libraries).

# Processes

Programs and processes appear similar on the surface, they are fundamentally different. A program is a static sequence of instructions, whereas a process is a container for a set of resources used when executing the instance of the process. At the highest level of abstraction, a Windows process comprises the following:

- A private virtual address space is a set of virtual memory addresses that the process can use.
- An executable program defines initial code and data and is mapped into the process's virtual address space.
- A list of open handles map to system resources such as semaphores, synchronization objects, and files that are accessible to all threads in the process.
- A security context is an access token that identifies the user, security groups, privileges, attributes, claims, capabilities, User Account Control (UAC) virtualization state, session, and limited user account state associated with the process, as well as the AppContainer identifier and its related sandbox information.
- A process ID is a unique identifier, which is internally part of an identifier called a client ID.
- At least one thread of execution Although an "empty" process is possible, it is (mostly) not useful.

A number of tools for viewing (and modifying) processes and process information are available. The following experiments illustrate the various views of process information you can obtain with some of these tools. While many of these tools are included within Windows, and within the Debugging Tools for Windows and the Windows SDK, others are stand-alone tools from Sysinternals. Many of these tools show overlapping subsets of the core process and thread information, sometimes identified by different names.
