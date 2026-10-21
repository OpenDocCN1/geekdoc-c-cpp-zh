
## Program D.7 REALIZING A REMOTE OBJECT

```
namespace Remote
{
using System;
public interface Remote
{
void Display();
}
```

The above code defines an interface named Remote containing the Display method prototype. To allow an application to extend this interface we must save it inside a library file (.dll). We can do that by using the /t:library option.

## Building a Server

To build the server side object, we need to first extend the Remote interface created above. We must also extend the MarshalByRefObject class to produce the remoting functionality, as shown below:

```
public class RemoteC : MarshalByRefObject, Remote
{
public void display ()
{
Console.WriteLine("Inside Server-Side Remote Object");
}
}
```

As explained earlier, the actual transfer of objects happens through a channel. So, we must create a channel on the server side for processing client requests, as shown below:

```
HttpChannel HC = new HttpChannel(50123);
ChannelServices.RegisterChannel(HC);
```

Here, we have created an HTTP channel at port 50123 for accepting client requests. The newly created channel must also be registered with the CLR through the ChannelServices.RegisterChannel method.

The final task in building a server side object is to register it using the RemotingConfiguration class, as shown below:

```
Type t = Type.GetType("RemoteC");
RemotingConfiguration.RegisterWellKnownServiceType(t, "EP", WellKnownObjectMode.Singleton);
```

Here, we have registered RemoteC as a well known singleton object.

## Building the Client

The building of client is a two-step process. First, it must register an HTTP channel for establishing a connection path with the remote object. Second, it must connect with the remote object using its URL, as shown below:

```
ChannelServices.RegisterChannel(new HttpChannel());
```

```
RemoteC R = (RemoteC)Activator.GetObject(typeof(RemoteC), "http://localhost:50123/EP");
R.display();
```

## Using SingleCall

While registering the server object we specified the WellKnownObjectMode.Singleton parameter to the RegisterWellKnownServiceType method. A singleton type object caters to multiple client requests simultaneously, thus enabling the applications to share data with each other.

We can change the type of a server object to SingleCall by passing WellKnownObjectMode.SingleCall parameter to the RegisterWellKnownServiceType method, as shown below:

```
Type t = Type.GetType("RemoteC");
RemotingConfiguration.RegisterWellKnownServiceType(t,"EP",WellKnownObjectMode.SingleCall );
```

This will produce a new instantiation for the server-side object every time a new client request is received.

## Appendix E

## Building C# Applications

There are a number of methods of building C# applications on the .NET Framework. While some of these methods ensure a programmer's efficiency through a comprehensive and robust development environment, such as Visual Studio IDE; other methods, such as csc.exe and other command line tools serve an entirely different purpose of experiencing program control at ground level.

In this appendix, we will learn how to build and debug C# applications at the command line.

C# compiler or csc.exe is a command line tool offered by the .NET Framework that allows you to build C# applications at the command prompt. While the mere knowledge of a .NET IDE is sufficient enough for a programmer to successfully build and deploy C# applications: it is at times advisable to learn how to manually build and debug the C# applications at the command line.

Some of the advantages of building C# applications at command line are the following:

- It helps a programmer explore the underlying mechanism of program execution on the .NET platform.
- It helps a programmer directly interact with the execution engine (csc.exe) without the intermediary IDE.
- By making use of debugging tools like cordbg.exe, one can explore how debugging is performed at command line.
- It helps a programmer to perform certain exclusive tasks, such as generation of multi-file assemblies, which are otherwise not supported by Visual Studio.
- Only the .NET SDK is sufficient enough to build C# applications and it is not required to install a full fledged IDE like Visual Studio.

The C# compiler can be initiated by typing the csc.exe command at the command prompt. But, before we start using the C# compiler, we need to set the environment path variable appropriately so that csc.exe can be executed from any subdirectory at the command line.

To set the environment path variable, you need to perform the following steps:

- 1. Right click the My Computer icon on the desktop to display a shortcut menu.

## Appendix E: Building C# Applications

Now, save the above program as Sample.cs. To run the Sample.cs program, you need to perform the following steps:

- 1. Open the command prompt window and open the directory where Sample.cs program is stored.
- 2. Type the following command at the command prompt:
  
  csc /out:Output.exe Sample.cs
  
  The C# compiler compiles the Sample.cs program and generates the Output.exe file at the same location.
- 3. Type Output.exe at the command prompt and press Enter to run the program. Fig. E.2 shows the output of Sample.cs program:

![](img/bae4ee2c7c29c052feb3b9a9c5659998_492_0.png)

## Fig. E.2 Output of Sample.cs program

## E.4 WORKING WITH CSC.EXE RESPONSE FILES

A command line instruction could become quite complex and error-prone if multiple files stored at different locations are to be compiled together; or if multiple external assemblies are to be referenced during compile time. To avoid such situations, C# supports the concept of response files. A response file stores all the flag settings before hand so that they are not required to be explicitly specified during compilation. Thus, a mere reference to the response file is sufficient enough for the C# compiler to load all the flag values at compile time.

To explore the functionality of response files let us create a .dll assembly and then refer it from the Sample.cs program using response files. Open a Notepad document and type the following code into it:

```
// The Library File
namespace ExternLib
{
using System;
public class ExternClass
{
public void display()
{
}
}
}
```

```
Console.WriteLine("Inside the display () method of ExternLib");
}
}
}
```

Save the above code file as ExternLib.cs. Now, to create an equivalent ExternLib.dll assembly, we must run the following command at the command prompt:

```
csc /t:library ExternLib.cs
```

Note the use of type library with the t flag that instructs the compiler to generate a .dll assembly named, ExternLib.dll.

Now, open the Sample.cs program that we created earlier and modify it as under:

```
//This is a Sample Program
using System; //System is a namespace
using ExternLib;
class Sample
{
public static void Main()
{
Console.WriteLine("Hello! Welcome to the world of C Sharp");
ExternClass e = new ExternClass();
e.display();
Console.WriteLine("....back to our main program....");
}
}
```

The above program creates an instance of the ExternClass class stored in the ExternLib.dll assembly and calls its display method. For the above code to run successfully, we must create a reference to the ExternLib.dll assembly at compile time. To create this reference using response files, you need to perform the following steps:

- 1. Open a Notepad document and type the following code into it:
  # This is a response file
  # Referencing external library
  /r:C:\ExternLib.dll
  # Specifying target assembly type
  /target:exe
  # Specifying target assembly name
  /out:Sample_Rsp.exe Sample.cs
  Note: The comments are specified inside a response file using # instead of /.
- 2. Save the above file as RspTest.rsp at the same location where the Sample.cs program is stored.
- 3. Type the following command at the command prompt to run the Sample.cs program using RspTest response file:
  csc @RspTest.rsp
- 4. On successful compilation, type the following command to run the Sample.cs program:
  Sample_Rsp.exe

Fig. E.3 shows the output of the Sample.cs program:
