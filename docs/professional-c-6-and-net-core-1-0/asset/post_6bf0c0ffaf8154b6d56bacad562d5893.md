
item template, the package.json file is added to the project:

```json
{
  "version": "1.0.0",
  "name": "ASP.NET",
  "private": "true",
  "devDependencies": {
  }
}
```

With the file open within Visual Studio, you can see the npm logo in the editor, as shown in Figure 40.6.

![](img/3d365b72b289213a91ade7eb366b8f35_1535_0.png)

**Figure 40.6**

> NOTE The package.json file is visible in the Solution Explorer only if you click the button Show All Files.

If you start adding JavaScript libraries to the devDependencies section of this file, the npm server is contacted as you type to allow completing the JavaScript library, and to show available version numbers. When you select the version number in the editor, you also get the offer for a ^ and ~ prefix. Without the prefix, exactly the version of the library with the exact name you typed is retrieved from the server. With the ^ prefix, the latest library with the same major version number is retrieved; with the ~ prefix, the latest library with the same minor version number is retrieved.

The following package.json file references a few gulp libraries and the rimraf library. As you save the package.json file, the npm packages are loaded from the server. In the Solution Explorer you can see the npm-loaded libraries in the Dependencies section. The Dependencies section has an npm child node where all the libraries loaded are shown.

```json
{
  "version": "1.0.0",
  "name": "ASP.NET",
  "private": "true",
  "devDependencies": {
    "gulp": "3.9.0",
    "gulp-concat": "2.6.0",
    "gulp-cssmin": "0.1.7",
    "gulp-uglify": "1.2.0",
    "rimraf": "2.4.2"
  }
}
```

What are these JavaScript libraries referenced good for? *gulp* is a build system that is discussed in the next section. *gulp-concat* concatenates JavaScript files; *gulp-cssmin* minifies CSS files; *gulp-uglify* minifies JavaScript files; and *rimraf* allows you to delete files in a hierarchy. Minification removes all unnecessary characters.

After the packages are added, you can easily update or uninstall the package using the npm node within the Dependencies section in Solution Explorer.

## Building with Gulp

*Gulp* is a build system for JavaScript. Whereas npm can be compared to NuGet, gulp can be compared to .NET Development Utility (DNU). JavaScript code is interpreted; why do you need a build system with JavaScript? There are a lot of things to do with HTML, CSS, and JavaScript before putting these files on the server. With a build system, you can convert Syntactically Awesome Stylesheets (SASS) files (CSS with scripting features) to CSS, you can minify and compress files, you can start unit tests for scripts, and you can analyze JavaScript code (for example, with JSHint)—there are a lot of useful tasks you can do.

After adding gulp with npm, a *Gulp Configuration File* can be added using a Visual Studio item template. This template creates the following gulp file (code file `MVCsampleApp/gulpfile.js`):

```javascript
/*
This file is the main entry point for defining Gulp tasks and
using Gulp plugins.
Click here to learn more. http://go.microsoft.com/fwlink/?
LinkId=518007
*/

var gulp = require('gulp');

gulp.task('default', function () {
    // place code for your default task here
});
```

The editor with the gulp logo is shown in [Figure 40.7](#figure-40.7).

```javascript
.pipe(cssmin())
.pipe(gulp.dest("."));
});

gulp.task("min", ["min:js","min:css"]);
```

Visual Studio 2015 offers a Task Runner Explorer (see [Figure 40.8](#figure-40.8)) for gulp files. Double-click on a task to start it. You can also map the gulp tasks to Visual Studio commands. This way gulp tasks are started automatically when a project is opened, before or after the build, or when the Clean menu entry is selected within the Build menu.

![](img/3d365b72b289213a91ade7eb366b8f35_1538_0.png)

[Figure 40.8](#figure-40.8)

> **NOTE** *Another JavaScript build system supported by Visual Studio is Grunt. The focus in Grunt is building via configuration, whereas the focus in Gulp is on building via JavaScript code.*

## Using Client-Side Libraries with Bower

Most client-side JavaScript libraries are available via *Bower*. Bower is a package manager like npm. Whereas the npm project started with JavaScript libraries for server-side code (although many client-side scripting libraries are also available with npm), Bower offers thousands of JavaScript client libraries.

Bower can be added to an ASP.NET web project by using the item template *Bower Configuration File*. This template adds the file `bower.json` as shown here:

```json
{
    "name":"ASP.NET",
    "private": true,
    "dependencies": {
    }
}
```

Adding Bower to the project also adds the `.bowerrc` file that configures Bower. By default, when you use the directory setting, the script files (as well as CSS and HTML files that come with the scripting libraries) are copied to the wwwroot/lib directory:

```json
{
  "directory":"wwwroot/lib"
}
```

> NOTE Similar to NPM, you need to click the Show All Files button in the Solution Explorer to see the bower-related files.

Visual Studio 2015 has special support for Bower. Figure 40.9 shows the Bower logo in the editor.

![](img/3d365b72b289213a91ade7eb366b8f35_1539_0.png)

**Figure 40.9**

If you start adding scripting libraries to the bower.json file, you get IntelliSense by typing both the name of the library and the version number. Similarly to npm, when you save the file, libraries are retrieved from the server and can be found within the Dependencies folder. Because of the configuration within .bowerrc, the files from the scripting libraries are copied to the wwwroot/lib folder (code file MVCSampleApp/.bowerrc):

```json
{
  "name":"ASP.NET",
  "private": true,
  "dependencies": {
    "bootstrap":"3.3.5",
    "jquery":"2.1.4",
    "jquery-validation":"1.14.0",
    "jquery-validation-unobtrusive":"3.2.5"
  }
}
```

Management of Bower packages is also available with the Manage Bower Packages tool that you can access by clicking the application context menu Manage Bower Packages. This tool is very similar to the NuGet Package Manager; it just makes it easy to manage Bower packages (see Figure 40.10).

![](img/3d365b72b289213a91ade7eb366b8f35_1540_0.png)

**Figure 40.10**

Now that the infrastructure is in place, it’s time to get into the HTTP request and response.

## Request and Response

With the HTTP protocol, the client makes a request to the server. This request is answered with a response.

The request consists of a header and, in many cases, body information to the server. The server uses the body information to define different results based on the needs of the client. Let’s have a look at what information can be read from the client.

To return an HTML-formatted output to the client, the GetDiv method creates a div element that contains span elements with the passed arguments key and value (code file WebSampleApp/RequestAndResponseSample.cs):

```csharp
public static string GetDiv(string key, string value) =>
  $"<div><span>{key}:</span><span>{value}</span></div>";
```

Because such HTML div and span tags are needed to surround strings in following examples, extension methods are created to cover this functionality (code file WebSampleApp/HtmlExtensions.cs):

```csharp
public static class HtmlExtensions
{
  public static string Div(this string value) =>
    $"<div>{value}</div>";

  public static string Span(this string value) =>
    $"<span>{value}</span>";
}
```

The method `GetRequestInformation` uses an `HttpRequest` object to access `Scheme`, `Host`, `Path`, `QueryString`, `Method`, and `Protocol` properties (code file `WebSampleApp/RequestAndResponseSample.cs`):

```csharp
public static string GetRequestInformation(HttpRequest request)
{
    var sb = new StringBuilder();
    sb.Append(GetDiv("scheme", request.Scheme));
    sb.Append(GetDiv("host", request.Host.HasValue ?
        request.Host.Value :
        "no host"));
    sb.Append(GetDiv("path", request.Path));
    sb.Append(GetDiv("query string", request.QueryString.HasValue
        ?
        request.QueryString.Value : "no query string"));

    sb.Append(GetDiv("method", request.Method));
    sb.Append(GetDiv("protocol", request.Protocol));

    return sb.ToString();
}
```

The `Configure` method of the `Startup` class is changed to invoke the `GetRequestInformation` method and pass the `HttpRequest` via the `Request` property of the `HttpContext`. The result is written to the `Response` object (code file `WebSampleApp/Startup.cs`):

```csharp
app.Run(async (context) =>
{
    await context.Response.WriteAsync(
        RequestAndResponseSample.GetRequestInformation(context.Request));
});
```

Starting the program from Visual Studio results in the following information:

```text
scheme:http
host:localhost:5000
path: /
query string: no query string
method: GET
protocol: HTTP/1.1
```

Adding a path, such as [http://localhost:5000/Index](http://localhost:5000/Index), to the request results in the path value set:

```text
scheme:http
host:localhost:5000
path: /Index
query string: no query string
method: GET
protocol: HTTP/1.1
```
