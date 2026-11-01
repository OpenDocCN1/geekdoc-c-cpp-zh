```
```csharp
dataRead, 0, dataRead.Length);
Dispatcher.BeginInvoke(new Action<string>(s =>
{
    textResult.Text = data;
}), data);
}
catch (WebException ex)
{
    Dispatcher.Invoke(new Action<string>(s =>
    {
        textResult.Text = s;
    }), ex.Message);
}, null);
```
```

code snippet WebRequestClient/WebRequestClient.xaml.cs

Now you can use several HTTP requests to the service and see the data returned. The running application is shown in Figure 32-3.

![](bbox=[0.12, 0.58, 0.72, 0.8])

# FIGURE 32-3

Using the request http://localhost:9000/Samples/Menus(3) to get the menu with the unique identifier 3, this AtomPub information is received:

```
```xml
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<entry xml:base="http://localhost:9000/Samples/"
xmlns:edm="http://schemas.microsoft.com/ado/2007/08/dataservices"
xmlns:edm="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"
xmlns="http://www.w3.org/2005/Atom">
<id>http://localhost:9000/Samples/Menus(3)</id>
<title type="text">title</title>
<updated>2009-07-30T12:20:07Z</updated>
<author>
<name />
</author>
<link rel="edit" title="Menu" href="Menus(3)" />
<link rel=
"http://schemas.microsoft.com/ado/2007/08/dataservices/related/Category"
type="application/atom+xml;type=entry" title="Category"
href="Menus(3)/Category" />
```
```