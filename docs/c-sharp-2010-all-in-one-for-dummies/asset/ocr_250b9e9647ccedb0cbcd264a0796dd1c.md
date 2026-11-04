# Chapter 4: Leveraging
the .NET Framework

# In This Chapter

+   ✔ Working with the .NET Framework
+   ✔ Dealing with requests
+   ✔ Using ASP.NET security
+   ✔ Using site maps
+   ✔ Managing files and cookies
+   ✔ Tracing and debugging

Let's be clear about ASP.NET and the .NET Framework. They are different. ASP.NET has a dependency on the .NET Framework, but it is really defined as the collection of controls that are in Chapter 3, plus others. The .NET Framework brings a different set of tools.

The controls that are in ASP.NET are user experience focused — they focus on the way the user views the application. The tools that are in the Framework are transport focused — focused on passing information back and forth between client and the server. If you look at the System.Web namespace (which is where most of these bits are stored), you'll quickly see that most of the classes within start with "Http." There is a reason for that: HTTP is the transport protocol.

This is important because manipulating the information that goes back and forth between the client and the server is the first and best way to do anything off-trail in a Web application. Whenever the default condition of the control or the server or the client isn't exactly what you need, the first place you turn is the classes of the System.Web namespace.

Controls in ASP.NET and controls in the .NET Framework overlap quite a bit, but each group is distinct. You should always keep in mind which tools are at your disposal and how best to use them.