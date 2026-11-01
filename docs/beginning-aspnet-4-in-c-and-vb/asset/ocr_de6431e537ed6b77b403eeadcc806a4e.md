As you have already learned, with ASP.NET you have to differentiate between the user interface culture and the culture used for formatting. Both of these cultures can be defined on a web and page level, as well as programmatically.

To be independent of the web server's operating system, the culture and user interface culture can be defined with the <globalization> element in the configuration file web.config:

```
```
<configuration>
  <system.web>
    <globalization culture="en-US" uiCulture="en-US" />
  </system.web>
</configuration>
```
```

code snippet WebApplication/Web.config

If the configuration should be different for specific web pages, the Page directive allows you to assign the culture:

```
```
<%@ Page language="C#" Culture="en-US" UICulture="en-US" %>
```
```

The user can configure the language with the browser. With Internet Explorer, this setting is defined with the Language Preference options (see Figure 22-13).

![](bbox=[0.58, 0.47, 0.92, 0.77])

FIGURE 22-13

If the page language should be set according to the language setting of the client, the culture of the thread can be set programmatically to the language setting that is received from the client. ASP.NET has an automatic setting that does just that. Setting the culture to the value Auto sets the culture of the thread according to the client's settings.

```
```
<%@ Page language="C#" Culture="Auto" UICulture="Auto" %>
```
```

In dealing with resources, ASP.NET differentiates resources that are used for the complete web site and resources that are needed only within a page.

If a resource is used within a page, you can create resources for the page by selecting the Visual Studio menu Tools → Generate Local Resource in the design view. This way, the subdirectory App_LocalResources is created, where a resource file for every page is stored. These resources can be localized similarly to the way they are in Windows applications. The association between the web controls and the local resource files is achieved by using a meta:resourcekey attribute, as shown here with the ASP.NET Label control. Label1Resource1 is the name of the resource that can be changed in the local resource file:

```
```
<asp:Label ID="Label1" runat="server" Text="English Text"
  meta:resourcekey="Label1Resource1"></asp:Label>
```
```

code snippet WebApplication/MultiLanguage.aspx

For the resources that should be shared between multiple pages, you have to create an ASP.NET folder, App_GlobalResources. In this directory, you can add resource files, for example, Messages.resx with its resources. To associate the web controls with these resources, you can use Expressions in the property editor. Clicking the Expressions button opens the Expressions dialog (see Figure 22-14). Here, you can select the expression type Resources, set the name of the ClassKey (which is the name of the resource file — here, a strongly typed resource file is generated), and the name of the ResourceKey, which is the name of the resource.

In the ASPX file, you can see the association to the resource with the binding expressions syntax <%=: