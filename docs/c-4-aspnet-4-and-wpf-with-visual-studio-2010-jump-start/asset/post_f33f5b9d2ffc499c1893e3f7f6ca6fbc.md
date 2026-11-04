
For example, the following code creates a Label. The Label.LayoutTransform element contains a RotateTransform that rotates the Label by 45 degrees.

```
<Label Canvas.Left="140" Canvas.Top="50" Background="LightGreen" Foreground="Red" Content="Rotate 45 degrees">
  <Label.LayoutTransform>
    <RotateTransform Angle="45" />
  </Label.LayoutTransform>
</Label>
```

The Transformations example program shown here demonstrates an assortment of transformations.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_114_0.png)

## EFFECTS

Much as transformations modify an object's geometry, bitmap effects modify the way in which an object is drawn.

To add an effect to an object, give it a BitmapEffect property element that contains an effect object. For example, the following code defines a Canvas that holds an Ellipse and a Path. The Canvas.BitmapEffect element holds a DropShadowBitmapEffect object to give the result a drop shadow.

```
<Canvas Width="100" Height="100">
  <Canvas.BitmapEffect>
    <DropShadowBitmapEffect />
  </Canvas.BitmapEffect>
  <Ellipse Stroke="Blue" Fill="Yellow" Width="100" Height="100" />
  <Path Data="M 20,50 A 30,180 1,0 80,50" Stroke="Blue" StrokeThickness="2" />
</Canvas>
```

The following list summarizes WPF's bitmap effect classes:

- BevelBitmapEffect — Adds beveled edges to the object.
- BlurBitmapEffect — Blurs the object. Radius determines how large the blurring is.
- DropShadowBitmapEffect — Adds a drop shadow behind the object.
- `EmbossBitmapEffect` — Embosses the object.
- `OuterGlowBitmapEffect` — Adds a glowing aura around the object.

If you want to use more than one effect at the same time, use a `BitmapEffect` element that contains a `BitmapEffectGroup`. Inside the `BitmapEffectGroup`, place the effects that you want to use. For example, the following code makes a `Canvas` use an `EmbossBitmapEffect` followed by a `BevelBitmapEffect`.

```
<Canvas.BitmapEffect>
    <BitmapEffectGroup>
        <EmbossBitmapEffect />
        <BevelBitmapEffect BevelWidth="10" />
    </BitmapEffectGroup>
</Canvas.BitmapEffect>
```

![](img/7954dcc7dd1d929d072aec8e9531b6cc_115_0.png)

*WPF Programmer's Reference 9780470477229 Effects*

The Effects example program shown in the next figure displays an unmodified object and the same object using the five basic bitmap effects. The final version shows the object using combinations of effects.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_115_1.png)

## DOCUMENTS

WPF documents can contain a wide variety of objects such as:

- Paragraphs
- Tables
- Lists
- Floaters
- Figures
- User interface elements such as `Buttons` and `TextBoxes`
- Three-dimensional objects

WPF has two different kinds of documents: fixed documents and flow documents.

### Fixed Documents

A *fixed document* displays its contents in exactly the same size and position whenever you view it. If you resize the control that holds the document, parts of the document may not fit, but they won't be moved. In that sense, this kind of document is similar to a PDF (Portable Document Format) file.

### Building XPS Documents

When it defined fixed documents, Microsoft also defined *XML Paper Specification (XPS)* files. An *XPS file* is a fixed document saved in a special format that can be read and displayed by certain programs such as recent versions of Internet Explorer.

One of the most flexible ways you can make an XPS document is to use Microsoft Word. Simply create a Word document containing any text, graphics, lists, or other content that you want, and then export it as an XPS document.

Microsoft Word 2007 can export files in XPS (or PDF) format, but you need to install an add-in first. As of this writing, you can install the add-in by following the instructions on Microsoft's "2007 Microsoft Office Add-in: Microsoft Save as PDF or XPS" download page at r.office.microsoft.com/r/rlidMSAddinPDFXPS. (If the page has moved so you can't find it, go to Microsoft's Download Center at www.microsoft.com/downloads and search for "Save as PDF or XPS.")

After you install the add-in, simply click on the Windows icon in Word's upper-left corner to expand the main file menu. Click on the arrow next to the "Save As" command, and select the "PDF or XPS" item.

If you don't have Microsoft Word but are running the Microsoft Windows 7 operating system, you can still create XPS documents relatively easily. Use Notepad, WordPad, or some other editor to create the document. Next print it, selecting Microsoft XPS Document Writer as the printer. The writer will prompt you for the file where you want to save the result.

You can even display a web page in a browser such as Firefox or Internet Explorer, print it, and select Microsoft XPS Document Writer as the printer.

### Displaying XPS Documents

After you have created an XPS file, you have several options for displaying it.

The Microsoft XPS Viewer, which is installed by default in Windows 7 and integrated into Internet Explorer 6.0 and higher, can display XPS files. By default, .xps files are associated with Internet Explorer, so you can probably just double-click on the file to view it.

You can also download Microsoft XPS Viewer or Microsoft XPS Essentials Pack (which contains a stand-alone viewer) at www.microsoft.com/whdc/xps/viewxps.mspx.

Finally, you can make a WPF application display an XPS file inside a `DocumentViewer` control. To do that, first add a reference to the ReachFramework library.

In Visual Studio, open the Project menu and select "Add Reference." On the Add Reference dialog, select the .NET tab, select the ReachFramework entry, and click OK.

Now you can write code-behind to load an XPS document into a `DocumentViewer` control. To make using the necessary classes easier, you can add the following `using` statement to the program:

```
    using System.Windows.Xps.Packaging;
```

The following code loads the file “Fixed Document.xps” when the program’s window loads:

![](img/7954dcc7dd1d929d072aec8e9531b6cc_117_0.png)

// Load the XPS document.
private void Window_Loaded(object sender, RoutedEventArgs e)
{
    // Note: Mark the file as "Copy if newer".
    // to make a copy go in the output directory.
    XpsDocument xps_doc = new XpsDocument("Fixed Document.xps",
        System.IO.FileAccess.Read);
    docViewer.Document = xps_doc.GetFixedDocumentSequence();
}

### Building Fixed Documents in XAML

Building an XPS document is easy with Microsoft Word, WordPad, or some other external program, but sometimes it’s more convenient to build a fixed document in XAML or code-behind. For example, you might want a program to generate a report at run time and display it as a fixed document.

Building a fixed document in XAML code isn’t too complicated, although it is a lot of work because it’s a fairly verbose format.

Start by creating a DocumentViewer to hold the document. Give it any properties and resources it needs (such as a background), and place a FixedDocument object inside it.

The FixedDocument object should contain one or more PageContent objects that define its pages.

You can set each PageContent object’s Width and Height properties to determine the size of the page.

Inside the PageContent, place a FixedPage object to define the page’s contents.

Inside the FixedPage, you can place controls such as StackPanel, Grid, TextBlock, and Border to create the page’s contents.

The SimpleFixedDocument example program shown in the next figure draws four fixed pages that contain simple shapes and labels.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_117_1.png)

### Saving XPS Files

Having gone to the trouble of building a fixed document in XAML or code-behind, you might want to save it as an XPS file.

To save a fixed document into an XPS file, open a project in Visual Studio and add references to the ReachFramework and System.Printing libraries. To make using the libraries easier, you can add the following using statements to the program:

```
using System.Windows.Xps;
using System.Windows.Xps.Packaging;
```

Next, create an XpsDocument object to write into the file that you want to create. Make an XpsDocumentWriter associated with the document object, and use its Write method to write the FixedDocument into the file.

The SaveFixedDocument example program uses the following code to save its FixedDocument object named fdContents into a file.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_118_0.png)

// Save as an XPS file.
private void mnuFileSave_Click(System.Object sender, System.Windows.RoutedEventArgs e)
{
    // Get the file name.
    Microsoft.Win32.SaveFileDialog dlg =
        new Microsoft.Win32.SaveFileDialog();
    dlg.FileName = "Shapes";
    dlg.DefaultExt = ".xps";
    dlg.Filter = "XPS Documents (.xps)|*.xps|All Files (*.*)|*.*";
    if (dlg.ShowDialog() == true)
    {
        // Save the document.
        // Make an XPS document.
        XpsDocument xps_doc = new XpsDocument(dlg.FileName,
            System.IO.FileAccess.Write);

        // Make an XPS document writer.
        XpsDocumentWriter doc_writer =
            XpsDocument.CreateXpsDocumentWriter(xps_doc);
        doc_writer.Write(fdContents);
        xps_doc.Close();
    }
}

### Flow Documents

A flow document rearranges its contents as necessary to fit the container that is holding it. If you make the viewing control tall and thin, the document reorganizes its contents to fit. In that sense, this kind of document is similar to a simple web page that rearranges its contents when you resize the browser.

A WPF program displays flow documents inside one of three kinds of viewers:
FlowDocumentPageViewer, FlowDocumentReader, or FlowDocumentScrollViewer. S
