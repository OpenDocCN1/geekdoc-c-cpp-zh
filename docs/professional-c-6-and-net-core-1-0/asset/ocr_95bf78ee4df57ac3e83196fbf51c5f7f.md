```
}
    }
}
```

The entry point for the web application is the Main method. With the emitEntryPoint configuration you’ve seen earlier in the project.json configuration file you can define if a Main method should be used. You also defined the Main method with .NET Core console applications created in this book. Only libraries don’t need a Main method.

With the default implementation as it is generated from the Visual Studio template, the web application is configured with the help of a WebHostBuilder instance. Using the WebHostBuilder, the method UseDefaultConfiguration is invoked. This method receives the command-line arguments and creates a configuration that includes the optional hosting file (hosting.json), adds environmental variables, and adds the command-line arguments to the configuration. The method UseStartup defines to use the Startup class, which in turn invokes the methods ConfigureServices and Configure. The last method invoked with the WebApplicationBuilder is the Build method, which returns an object implementing the interface IWebApplication. With the returned application object, the Run method is invoked, which starts the hosting engine; now the server is listening and waiting for requests.

The hosting.json file is used to configure the server (code file WebSampleApp/hosting.json):

```
{
    "server":"Microsoft.AspNetCore.Server.Kestrel",
    "server.urls":"http://localhost:5000"
}
```

Because the Startup class is passed to the UseStartup method with a generic template parameter, in turn the methods ConfigureServices and Configure are invoked.

The Configure method receives an internal application builder type via dependency injection that implements the interface IApplicationBuilder. This interface is used to define services used by the application. Calling the Use method of this interface, you can build the HTTP request pipeline to define what should be done in answer to a request. The Run method is an extension method for the interface IApplicationBuilder; it invokes the Use method. This method is implemented via the RunExtensions extension class in the assembly Microsoft.AspNetCore.Http.Abstractions and the namespace Microsoft.AspNetCore.Builder.

The parameter of the Run method is a delegate of type RequestDelegate. This type receives an HttpContext as a parameter, and it returns a Task. With the HttpContext (the context variable in the code snippet), you have access to the request information from the browser (HTTP headers, cookies, and form data) and can send a response. The code snippet returns a simple string—Hello, World!—to the client, as shown