
# WINDOWS PRESENTATION FOUNDATION

While Silverlight is a trimmed down, smaller version of WPF and the .NET Framework, WPF aims to be complete. In Silverlight, there is usually only one way to do things; WPF offers several approaches to the same problem.

The HelloWorld application in WPF looks very similar to the Silverlight version at the beginning of this chapter. Listing 8-19 shows the XAML for the WPF version:

+ LISTING 8-19: MainWindow.xaml

```xml
<Window x:Class=HelloWorld
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Height="350" Width="525">
<Grid>
  <TextBlock Text="Hello, World!" HorizontalAlignment="Center" VerticalAlignment="Center" />
</Grid>
</Window>
```

Code file [MainWindow.xaml] available for download at Wrox.com.

The Grid control and its TextBlock content are exactly the same as in the Silverlight version. Even the XAML namespaces are the same. The only difference is with the root element; with WPF, it is Window.

The other key difference occurs when running the application. Instead of a browser and a plug-in, you get a full desktop application, as shown in Figure 8-37.

WPF applications can also run within the browser. This is called XBAP deployment. However, running a WPF application in the entire .NET Framework to be installed on the user's computer, and, thus, only works in Windows (while Silverlight works on other platforms, and only needs the Silverlight plug-in).

> Figure 8-37: The HelloWorld application

![](img/b5597c749e848b27b0d305153ae16106_400_0.png)

To create an XBAP application, you must choose WPF Browser Application in the New Project dialog of Visual Studio 2010, as shown in Figure 8-38.

![](img/b5597c749e848b27b0d305153ae16106_401_0.png)

FIGURE 8-38: Creating a WPF Browser (XBAP) Application in Visual Studio

Figure 8-39 shows what a HelloWorld WPF XBAP application looks like in the browser.

![](img/b5597c749e848b27b0d305153ae16106_401_1.png)

FIGURE 8-39: An XBAP application in the Browser

WPF 4 also introduced running XBAP applications in full-trust mode, and access to the HTML Document Object Model (DOM) via the BrowserInteropHelper class.

As you can see from the previous sample, the key principles and pillars of Silverlight also apply to WPF. The most important features that Silverlight and WPF do not (at least in version 4) are smooth streaming, Deep Zoom, easy webcam and microphone access, and of course, cross-platform compatibility.

## WPF Features Not Available in Silverlight

This section introduces some of the unique WPF features not found in Silverlight. This examination is by no means complete, because the WPF platform is a lot more comprehensive than Silverlight. Rather, this discussion provides just a subjective selection.

## Rich Document Presentation with Flow Documents

Flow documents allow displaying rich document content in an adaptive way. Flow documents can adapt to changes in window size and font size to suit many different viewing scenarios. In Figure 8-40, you can see the SDK viewer demo from the MSDN Library (http://msdn.microsoft.com/en-us/library/aa972141.aspx) adapts.

![](img/b5597c749e848b27b0d305153ae16106_402_0.png)

**FIGURE 8-40:** In a narrow window, FlowDocument displays one column; in a wider window two columns; and in a wide window it reverts to one column

The FlowDocument class are usually paragraphs, lists, sections, tables, and so on. A FlowDocument can contain any WPF UIElement, as buttons, images, or even media players.

When a FlowDocument is placed within a FlowDocumentReader, UI for paging, search, searching viewing mode, and zooming content are also displayed. Of course, these features can be customized or turned off. Here is a simple FlowDocument XML code snippet:

```xml
<FlowDocumentReader>
  <FlowDocument>
    <Paragraph>Hello, World!</Paragraph>
    <Paragraph>This is the FlowDocument demo.</Paragraph>
    <Paragraph>
      This is an inline calendar:
      <Calendar />
      And the text goes here...
    </Paragraph>
  </FlowDocument>
</FlowDocumentReader>
```

Figure 8-41 shows this code running.

![](img/b5597c749e848b27b0d305153ae16106_403_0.png)

**FIGURE 8-41:** FlowDocument sample with an interactive Calendar control inline

Combined with the new font-rendering capabilities of WPF 4, flow documents can provide an excellent reading experience.

## Additional Layout Containers and Controls

While WrapPanel made its way into the Silverlight Toolkit, Viewbox is now in the core — ListView, DockPanel, and UniformGrid.

The FlowDocument class are usually paragraphs, lists, sections, tables, and so on. A FlowDocument can contain any WPF UIElement, as buttons, images, or even media players.

When a FlowDocument is placed within a FlowDocumentReader, UI for paging, search, searching viewing mode, and zooming content are also displayed. Of course, these features can be customized or turned off. Here is a simple FlowDocument XML code snippet:

## Additional Layout Containers and Controls

While WrapPanel made its way into the Silverlight Toolkit, Viewbox is now in the core — ListView, DockPanel, and UniformGrid.
