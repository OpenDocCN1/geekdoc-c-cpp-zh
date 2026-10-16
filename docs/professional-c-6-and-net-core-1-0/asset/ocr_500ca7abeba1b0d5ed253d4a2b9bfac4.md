![](bbox=[0.1, 0.06, 0.9, 0.36])

# Figure 41.1

With ASP.NET MVC, the controller and model are typically created with C# and .NET code that is run server-side. The view is HTML code with JavaScript and just a little C# code for accessing server-side information.

The big advantage of this separation in the MVC pattern is that you can use unit tests to easily test the functionality. The controller just contains methods with parameters and return values that can be covered easily with unit tests.

Let’s start setting up services for ASP.NET MVC 6. With ASP.NET Core 1.0 dependency injection is deeply integrated as you’ve seen in Chapter 40. You can create an ASP.NET MVC 6 project selecting the ASP.NET Core 1.0 Template Web Application. This template already includes NuGet packages required with ASP.NET MVC 6, and a directory structure that helps with organizing the application. However, here we’ll start with the Empty template (similar to Chapter 40), so you can see what’s all needed to build up an ASP.NET MVC 6 project, without the extra stuff you might not need with your project.

The first project created is named MVCSampleApp. To use ASP.NET MVC with the web application MVCSampleApp, you need to add the NuGet package Microsoft.AspNet.Mvc. With the package in place, you add the MVC services by invoking the extension method AddMvc within the ConfigureServices method (code file MVCSampleApp/Startup.cs):

```
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
// etc.

namespace MVCSampleApp
```