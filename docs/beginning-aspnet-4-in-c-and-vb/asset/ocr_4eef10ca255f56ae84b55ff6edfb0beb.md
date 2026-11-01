# ASP.NET INTRODUCTION

ASP.NET works with Internet Information Services (IIS) to deliver content in response to HTTP requests. ASP.NET pages are found in .aspx files. Figure 40-1 illustrates the technology's basic architecture.

![](bbox=[0.1, 0.26, 0.88, 0.52])

FIGURE 40-1

# How ASP.NET Files are Processed

During ASP.NET processing, you have access to all .NET classes, custom components created in C# or other languages, databases, and so on. In fact, you have as much power as you would have running a C# application; using C# in ASP.NET is, in effect, running a C# application.

An ASP.NET file can contain any of the following:

+   - Processing instructions for the server
+   - Code in C#, Visual Basic .NET, JScript .NET, or any other language that the .NET Framework supports
+   - Content in whatever form is appropriate for the generated resource, such as HTML
+   - Client-side script code, such as JavaScript
+   - Embedded ASP.NET server controls

So, in fact, you could have an ASP.NET file as simple as this:

```
Hello!
```

This would simply result in an HTML page being returned (as HTML is the default output of ASP.NET pages) containing just this text.

As you will see later in this chapter, it is also possible to split certain portions of the code into other files, which can provide a more logical structure.

# Web Sites and Web Applications

In ASP.NET it is possible to create both “web sites” and “web applications”. These two terms both mean that you supply a collection of ASP.NET, C#, and other files, but the way that they are processed is subtly different.

In a web site, any code that you supply is dynamically compiled as and when it is required. This generally means that code is compiled the first time that the site is accessed. The .cs files for a web site are stored on the web server, which means that you can make changes by uploading new versions of these files, which will trigger a recompile the next time the site is accessed.