![](bbox=[0.145, 0.082, 0.802, 0.42])

# FIGURE 24-23

The server object model is implemented in the Microsoft.SharePoint.dll. Add a reference to this assembly, which you'll find on the .NET tab of the Add Reference dialog.

Getting back to the code for the console application, the first thing you need to do is get access to the site you want to inspect. You can't create a SPWeb object directly, so you need to get an object representing the parent site collection and use one of its properties or methods. Because the site we want is the root site in the collection, we'll use the RootWeb property.

Update Module1.vb to look like the following:

```
Imports Microsoft.SharePoint

Module Module1
    Sub Main()
        Dim siteUrl = "http://localhost/sites/demo/"
        Using site As New SPSite(siteUrl)
            Dim web = site.RootWeb

        End Using
    End Sub
End Module
```

Code snippet from Module1.vb

Note that the SPSite object is instantiated with a Using statement. Both the SPSite and SPWeb objects hold references to unmanaged resources that need to be cleaned up in a timely manner. Not doing so can have significant adverse effects on the performance and resource usage of your applications. The rule of thumb is that if you create an instance of an SPSite or SPWeb, you should ensure that it is disposed. If you get a reference to the SPSite or SPWeb from a property of another object, you should not dispose.