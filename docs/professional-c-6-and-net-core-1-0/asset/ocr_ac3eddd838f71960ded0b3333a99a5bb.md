# 40

# ASP.NET Core

# What’s In This Chapter?

+   - Understanding ASP.NET Core 1.0 and Web Technologies
+   - Using Static Content
+   - Working with HTTP Request and Response
+   - Using Dependency Injection with ASP.NET
+   - Defining Custom Simple Routing
+   - Creating Middleware Components
+   - Using Sessions for State Management
+   - Reading Configuration Settings

# Wrox.com Code Downloads for This Chapter

The wrox.com code downloads for this chapter are found at http://www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter contains this example project: WebSampleApp.

# ASP.NET Core 1.0

After 15 years of ASP.NET, ASP.NET Core 1.0 is a complete rewrite of ASP.NET. It features modular programming, is fully open sourced, is lightweight for best use on the cloud, and is available to non-Microsoft platforms.

A full rewrite of ASP.NET gives a lot of advantages, but this also means reworking existing web applications based on older versions of ASP.NET. Is it necessary to rewrite existing web applications to ASP.NET Core 1.0? Let’s try to answer this question.

ASP.NET Web Forms is no longer part of ASP.NET Core 1.0. However, having web applications that include this technology does not mean you have to rewrite them. It’s still possible to maintain legacy applications written with ASP.NET Web Forms with the full framework. ASP.NET Web Forms even received some enhancements with the newest version ASP.NET 4.6, such as asynchronous model binding.

ASP.NET MVC is still part of ASP.NET Core 1.0. Because ASP.NET MVC 6 has been completely rewritten, you need to make some changes to web applications written with ASP.NET MVC 5 or older versions to bring them to the new application stack.

Converting ASP.NET Web Forms to ASP.NET MVC might be a lot of work. ASP.NET Web Forms abstracts HTML and JavaScript from the