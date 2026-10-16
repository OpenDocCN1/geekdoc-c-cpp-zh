
```
WriteLine(programResources.GetString("Resource1"));
```

## The System.Resources Namespace

Before moving on to the next example, this section provides a review of the classes contained in the System.Resources namespace that deal with resources:

- ResourceManager—Can be used to get resources for the current culture from assemblies or resource files. Using the ResourceManager, you can also get a ResourceSet for a particular culture.
- ResourceSet—Represents the resources for a particular culture. When a ResourceSet instance is created, it enumerates over a class, implementing the interface IResourceReader, and it stores all resources in a Hashtable.
- IResourceReader—Used from the ResourceSet to enumerate resources. The class ResourceReader implements this interface.
- ResourceWriter—Used to create a resource file. ResourceWriter implements the interface IResourceWriter.

## Localization with WPF

With WPF, you can use .NET resources, similar to what you’ve seen with console applications. To see the use of resources with a WPF application, create a simple WPF application containing just one button, as shown in Figure 28.7.

![](img/3d365b72b289213a91ade7eb366b8f35_1047_0.png)

Figure 28.7

The XAML code for this application is shown here:

```
<Window x:Class="WpfApplication.MainWindow"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="WPF Sample" Height="350" Width="525">
<Grid>
    <Button Name="button1" Margin="30,20,30,20"
            Click="Button_Click"
            Content="English Button" />
</Grid>
</Window>
```

With the handler code for the `click` event of the button, only a message box containing a sample message pops up:

```
private void Button_Click(object sender, RoutedEventArgs e)
{
    MessageBox.Show("English Message");
}
```

> **NOTE** *You can read more about WPF and XAML in Chapter 29, “Core XAML,” and Chapter 34, “Windows Desktop Applications with WPF.”*

You add .NET resources to a WPF application similarly to how you add them to other applications. Define the resources named `Button1Text` and `Button1Message` in the file `Resources.resx`. This file is automatically created with a WPF project. You can find it in the `Properties` folder in Solution Explorer. By default, this resource file has an `Internal` access modifier to create the `Resources` class. To use it from within XAML, you must change this to `Public` within the Managed Resources Editor. While selecting the resource file and opening the Properties Window, you can see that the custom tool `PublicResXFileCodeGenerator` is assigned to the file. This code generator creates a strongly typed code file to access the resources. The generated code file offers public static properties with the name of the resource keys that accesses a `ResourceManager` as you can see with the `Button1Text` property in the following code snippet. The `ResourceManager` used here is a property that returns an instance of the `ResourceManager` class, which is created using a Singleton pattern:

```
public static string Button1Text
{
    get
    {
        return ResourceManager.GetString("Button1Text",
            resourceCulture);
    }
}
```

To use the generated resource class, you need to change the XAML code. Add an XML namespace alias to reference the .NET namespace `WpfApplication.Properties` as shown in the following code. Here, the alias is set to the value `props`. From XAML elements, properties of this class can be used with the `x:Static` markup extension. The `Content` property of the `Button` is set to the `Button1Text` property of the `Resources` class (code file `WPFApplication\MainWindow.xaml`):

```
<Window x:Class="WpfApplication.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:props="clr-namespace:WpfApplication.Properties"
    Title="WPF Sample" Height="350" Width="525">
<Grid>
    <Button Name="button1" Margin="30,20,30,20"
            Click="Button_Click"
            Content="{x:Static Member=props:Resources.Button1Text}" />
</Grid>
</Window>
```

To use the .NET resource from code-behind, just access the Button1Message property directly (code file WPFApplication\MainWindow.xaml.cs):

```
private void Button_Click(object sender, RoutedEventArgs e)
{
    MessageBox.Show(Properties.Resources.Button1Message);
}
```

Now the resources can be localized as before.

## Localization with ASP.NET Core

> **NOTE** For using localization with ASP.NET Core, you need to know about both cultures and resources that are discussed in this chapter as well as creating ASP.NET Core applications. In case you didn’t create ASP.NET Core web applications with .NET Core before, you should read Chapter 40, “ASP.NET Core,” before continuing with this part of the chapter.

For localization of ASP.NET Core web applications, you can use the CultureInfo class and resources similar to what you’ve seen earlier in this chapter, but there are some additional issues that you need to resolve. Setting the culture for the complete application doesn’t fulfill usual needs because users are coming from different cultures. So it’s necessary to set the culture with every request to the server.

How do you know about the culture of the user? There are different options. The browser sends preferred languages within the HTTP header with every request. This information from the browser can come from browser settings or when the browser itself checks the installed languages. Another option is to define URL parameters or use different domain names for different languages. You can use different domain names in some scenarios, such as www.cninnovation.com for an English version of the site and www.cninnovation.de for a German version. But what about www.cninnovation.ch? This should be offered both in German and French and probably Italian. URL parameters such

## Culture Providers

Let’s get into more details on these culture providers. The `QueryStringRequestCultureProvider` uses the query string to retrieve the culture. By default, the query parameters `culture` and `ui-culture` are used with this provider, as shown with this URL:
http://localhost:5000/?culture=de&ui-culture=en-US

You can also change the query parameters by setting the `QueryStringKey` and `UIQueryStringKey` properties of the `QueryStringRequestCultureProvider`.

The `CookieRequestCultureProvider` defines the cookie named `ASPNET_CULTURE` (which can be set using the `CookieName` property). The values from this cookie are retrieved to set the culture. To create a cookie and send it to the client, you can use the static method `MakeCookieValue` to create a cookie from a `RequestCulture` and send it to the client. The `CookieRequestCultureProvider` uses the static method `ParseCookieValue` to get a `RequestCulture`.

With the third option for culture settings, you can use the HTTP header information that is sent by the browser. The HTTP header that is sent looks like this:

`Accept-Language: en-us, de-at;q=0.8, it;q=0.7`

The `AcceptLanguageHeaderRequestCultureProvider` uses this information to set the culture. You use up to three language values in the order as defined by the quality value to find a first match with the supported cultures.

The following code snippet now uses the request culture to generate HTML output. First, you access the requested culture using the `IRequestCultureFeature` contract. The `RequestCultureFeature` that implements the interface `IRequestCultureFeature` uses the first culture provider that matches the culture setting. If a URL defines a query string that matches the culture parameter, the `QueryStringRequestCultureProvider` is used to return the requested culture. If the URL does not match, but a cookie with the name `ASPNET_CULTURE` is received, the `CookieRequestCultureProvider` is used, and otherwise the `AcceptLanguageHeaderRequestCultureProvider`. The resulting culture that is used by the user is written to the response stream using properties of the returned `RequestCulture`. Then, today’s date is written to the stream using the current culture. The variable of type `IStringLocalizer` used here needs some more examination next:

```
public void Configure(IApplicationBuilder app,
    IStringLocalizer<Startup> sr)
{
    // etc.

    app.Run(async context =>
    {
        IRequestCultureFeature requestCultureFeature =
```

