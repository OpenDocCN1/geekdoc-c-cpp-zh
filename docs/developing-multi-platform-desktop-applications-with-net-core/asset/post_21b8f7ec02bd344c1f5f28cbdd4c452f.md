
- 1. Building the request.
- 2. Processing the request and retrieve data (results).
- 3. Processing the results.

## 5.4.1 Building the Web request

First you will have to specify the endpoint address, once it is done you will instantiate the HttpClient class doing the web request. This API support only async methods (useful when you work on the network). The task web request will be performed by an async method (see sample code for REST Client).

## 5.4.2 Processing the request and retrieve data

The call of the web request will be done with the await keyword (that's an async method).

## 5.4.3 Processing JSON result

Once you have retrieved the data from the REST service (HTTP status 200), you will have to convert the JSON result into exploitable C# object. For doing that you have to write a class for the type of the object matching the JSON result format you expect.

TIPS: In Visual Studio use the menu Edit/Paste special/paste code as class for generating C# object from JSON data.

Once the class is defined you just have to use the method DeserializeObject to instantiate your class with the values of your result.

## 5.4.4 Sample code for a REST client

Here is a snippet for illustrating the use of a REST web service in your .NET Core 3 application.

### ProgramRESTClient.cs

```
BasicHttpBinding basicHttpBinding = null;
EndpointAddress endpointAddress = null;
ChannelFactory<IAService> factory = null;
IAService serviceProxy = null;
try
{
    basicHttpBinding = new BasicHttpBinding(BasicHttpSecurityMode.Transport);
    basicHttpBinding.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    endpointAddress = new EndpointAddress(new Uri("https://uri.com/api/"));
    factory = new ChannelFactory<IAService>(basicHttpBinding, endpointAddress);
    factory.Credentials.UserName.UserName = "usr";
    factory.Credentials.UserName.Password = "pass";
    serviceProxy = factory.CreateChannel();
    using (var scope = new OperationContextScope((IContextChannel)serviceProxy))
    {
        var result = await serviceProxy.getSomethingAsync("id").ConfigureAwait(false);
        factory.Close();
        ((ICommunicationObject)serviceProxy).Close();
    }
}
catch (MessageSecurityException ex)
{
    throw;
}
catch (Exception ex)
{
    throw;
}
```

## 5.5 THREADING GUI

As we have seen in the previous chapter, the reactivity of an application is a crucial metric of the user's global quality perception of a desktop application.

The good reactivity of the application can be reached by giving to each heavy processing task and User Interface task its own thread. Thus, the main process is never overloaded and the application continue to respond to the user (reactivity), whatever the previous instructions.

There are several methods for achieving this threading according to the type of solution you want to use for developing your multiplatform application (Console, XAML, HTML, Native UI ...).

The threading of long and complex task of your application can be done in a progress window where you display a gauge (or other progress indicator) control and propose to the user the option to Cancel the operation in progress.

![](img/3d310cc066dda6e2dfa67a650614076f_83_0.png)

(Sample Progress Window)

But most of the time the threading does not have its own window and report to the application the status of the operation through some kind of information bar. This can be done by using delegates and common threading techniques (as illustrated in the following sample).

The following simple .NET Core 3 WinForms example illustrates how it can be done by the use of delegate:

![](img/3d310cc066dda6e2dfa67a650614076f_84_0.png)

(UI_Threading_Example)

This sample illustrates the usefulness of the use of threading in GUI application compared to the non-threaded method that freezes the form (the user lost control) during the execution of the process.

The complete project of this example is available online.

> https://github.com/netcore3/CodeBook/Chapter 5/5/UI_Threading_Example

There are many other ways to implement (to code) the threading in your GUI, consider only that you should implement the processing of the functional operations outside the main GUI thread of your program (the method used is not really important, many different methods for doing that” are presented along this book).

## 5.6 USING UNMANAGED DEPENDENCIES

The multiplatform development with .NET Core 3 will sometimes imply the use of platform-specific dependencies (.dll files with Windows, .so file with ubuntu, .dylib file with macOS).

The capability for the developer to access unmanaged methods from his .NET Core 3 program is mandatory for conducting many types of projects.

You have to keep in mind that, in the multiplatform context, you have to get the native library file (or its equivalent for the platform) for each platform, in our case Linux, macOS, Windows.

So, verify if the library you plan to use for your multiplatform project will be available for each OS you target before actually using it in your development on the Windows platform.

For example, many system functions are accessible only through native API, for doing so you should know basic concepts for the use of unmanaged code with .NET Core 3 (which is managed code):

- P/Invoke
- Marshalling
- Establishing the running OS

The .NET Core 3 package providing these features is:

## 5.6.1 P/Invoke

P/Invoke is an acronym for Platform Invocation Services, this mechanism allows the developer to use external unmanaged dependencies in his managed code (.NET Core).

Here is a sample of the use of P/Invoke for retrieving the current process ID (pid):

### For Linux (ubuntu):

```
using System.Runtime.InteropServices;

namespace PInvokeSample
{
    public static class Program
    {
        [DllImport("libc.so.6")]
        private static extern int getpid();
        public static void Main(string[] args)
        {
            int pid = getpid();
            Console.WriteLine(pid);
        }
    }
}
```

### For Windows:

```
using System.Runtime.InteropServices;

namespace PInvokeSample
{
    public static class Program
    {
        [DllImport("Kernel32.dll")]
        private static extern uint GetCurrentThreadId();
        public static void Main(string[] args)
        {
            int pid = GetCurrentThreadId();
            Console.WriteLine(pid);
        }
    }
}
```

For this sample code: retrieving the current process ID, it is better to make a copy of the dependencies in the folder of the application. A tricky part for using system native libraries in your code is to retrieve the location of these libraries in each system. That's a point where you can encounter many troubles and the copy of the libraries in the project folder (or in a subfolder in the project) can help you to solve most of these issues. You have also to verify that the paths of the project context contain the required libraries for the OS where your application should be executed.

In the previous sample we can see that the native calls are changing according to the OS, in this case multiplatform development means producing the code for each platform specifics.

If you want to use native functions that are not already written and accessible in the system API of the OS, you have to develop your own libraries (one version for each OS).

Here is some reference links about the systems APIs for each OS.

- Windows: http://pinvoke.net
- Linux (ubuntu): http://kernel.org/doc/html/latest
- macOS: https://developer.apple.com/library/archive/navigation/

## 5.6.2 Marshalling

Marshalling: is the process of transforming types when it's needed to allow cross between native code and managed (in our case .NET Core 3) code.

Here is the table of the type conversion to use with .NET Core 3 types and native's types.

| .NET Type | Native Type |
| :--- | :--- |
| byte | uint8_t |
| sbyte | int8_t |
| short | int16_t |
| ushort | uint16_t |
| int | int32_t |
| uint | uint32_t |
| long | int64_t |
| ulong | uint64_t |
| char | Either char or char16_t depending on the CharSet of the P/Invoke or structure. |
| string | Either char* or char16_t* depending on the CharSet of the P/Invoke or structure. |
| System.IntPtr | intptr_t |
