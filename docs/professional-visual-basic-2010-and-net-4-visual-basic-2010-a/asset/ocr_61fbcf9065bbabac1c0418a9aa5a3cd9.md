same external assembly to exist side by side. For example, an application could use a newer version of ADO.NET without adversely affecting another application that relies on a previous version.

As long as the client has the .NET runtime installed (which only has to be done once), a .NET application can be distributed using a simple command like this:

```
xcopy \\server\appDirectory "C:\Program Files\appDirectory" /E /O /I
```

The preceding command would copy all of the files and subdirectories from \\server\appDirectory to C:\Program Files\appDirectory and would transfer the file’s access control lists (ACLs).

Besides the capability to copy applications, Visual Studio provides a built-in tool for constructing simple .msi installations. The deployment settings can be customized for your project solution, enabling you to integrate the deployment project with your application output. Additionally, Visual Studio 2005 introduced the capability to create a “ClickOnce” deployment.

ClickOnce deployment provided an entirely new method of deployment, referred to as *smart-client deployment*. In the smart-client model, your application is placed on a central server from which the clients access the application files. Smart-client deployment builds on the XML Web Services architecture about which you are learning. It has the advantages of central application maintenance combined with a richer client interface and fewer server communication requirements, all of which you have become familiar with in Windows Forms applications.

# CROSS-LANGUAGE INTEGRATION

Prior to .NET, interoperating with code written in other languages was challenging. There were pretty much two options for reusing functionality developed in other languages: COM interfaces or DLLs with exported C functions. As for exposing functionality written in Visual Basic, the only option was to create COM interfaces.

Because Visual Basic is now built on top of the CLR, it’s able to interoperate with the code written in other .NET languages. It’s even able to derive from a class written in another language. To support this type of functionality, the CLR relies on a common way of representing types, as well as rich metadata that can describe these types.

# The Common Type System

Each programming language seems to bring its own island of data types with it. For example, previous versions of Visual Basic represent strings using the basic, or binary, string (BSTR) structure, C++ offers the char and wchar data types, and MFC offers the CString class. Moreover, because the C++ int data type is a 32-bit value, whereas the Visual Basic 6 Integer data type is a 16-bit value, that makes it difficult to pass parameters between applications written using different languages.

To help resolve this problem, C has become the lowest common denominator for interfacing between programs written in multiple languages. An exported function written in C that exposes simple C data types can be consumed by Visual Basic, Java, Delphi, and a variety of other programming languages. In fact, the Windows API is exposed as a set of C functions.

Unfortunately, to access a C interface, you must explicitly map C data types to a language’s native data types. For example, a Visual Basic 6 developer would use the following statement to map the GetUserNameA Win32 function (GetUserNameA is the ANSI version of the GetUserName function):

```
’ Map GetUserName to the GetUserNameA exported function
’ exported by advapi32.dll.
’     BOOL GetUserName(
’         LPTSTR lpBuffer, // name buffer
’         LPDWORD nSize // size of name buffer
’     );
Public Declare Function GetUserName Lib "advapi32.dll" _
Alias "GetUserNameA" (ByVal strBuffer As String, nSize As Long) As Long
```