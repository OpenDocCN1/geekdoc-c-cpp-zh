
**Table 6.26: Values of the Properties of the Label, Button, and Text Box Controls**

| Control | Property | Value |
|---|---|---|
|  | Size | 75, 23 |
| textBox1 | Multiline | True |
|  | Location | 28, 77 |
|  | Size | 222, 91 |

5. Drag the **PrintDocument** and **PrintDialog** controls from the **Printing** tab of **Toolbox** and drop them on the **Form1** form, as shown in Fig.C.6-41:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_216_0.png)

As you can see in Fig.C.6-41, both the **PrintDocument** and the **PrintDialog** controls appear in the component tray.

6. Double-click the **button1** button to add the highlighted code, as given in Listing 6.10, in its **Click** event handler in the **Form1.cs** file.

7. Switch to the designer of the **Form1** form and double-click the **printDocument1** control in the component tray. The **PrintPage** event handler of the **printDocument1** control is added to the **Form1.cs** file.

Listing 6.10 shows the highlighted code to be added for the Click event handler of the **button1** button and the PrintPage event handler of the **printDocument1** control:

**Listing 6.10: Showing the Code of the button1_Click and printDocument1_PrintPage Event Handlers**

```csharp
private void button1_Click(object sender, EventArgs e) {
    printDocument1.DocumentName = "My Custom Document";
    printDialog1.Document = printDocument1;
    printDialog1.AllowSomePages = true;
    printDialog1.AllowCurrentPage = true;
    if (printDialog1.ShowDialog() == DialogResult.OK) {
        printDocument1.PrinterSettings = printDialog1.PrinterSettings;
        printDocument1.Print();
    }
}

private void printDocument1_PrintPage(object sender,
    System.Drawing.Printing.PrintPageEventArgs e)
{
    Font fontText = new Font("Arial", 14, FontStyle.Bold);
    e.Graphics.DrawString(textBox1.Text, fontText, Brushes.Black, new Rectangle(50, 50,
        e.PageBounds.Height, e.PageBounds.Width));
}
```

In Listing 6.10, you see that in the **button1_Click** event handler, the **DocumentName** property of the **printDocument1** control is set to **My Custom Document**. This implies that **My Custom Document** is displayed as the name of document at the time of printing. In addition, the **Document** property of the **printDialog1** control is set to **printDocument1**, implying that the output to the printer selected in the Print dialog box is sent by the **printDocument1** control. Both, the **AllowSomePages** and the **AllowCurrentPage** properties of the **printDialog1** control are set to **true**; which implies that the **Print** dialog box provides the users with the facility to print a sequence of pages as well as only the current page, respectively. When the **if** statement is true, that is, when the user clicks the **Print** button (equivalent to the **OK** button in other dialog boxes) in the **Print** dialog box, the printer settings specified in the **Print** dialog box are applied to the **printDocument1** control and the **Print()** method of the **printDocument1** control is called to start printing.

In the **printDocument1_PrintPage** event handler, various settings for printing the document are set. The **Font**, **Brushes**, and **Rectangle** classes of the **System.Drawing** namespace are used to print the document. Therefore, to use these three classes, you must include the **System.Drawing** namespace in your **Form1.cs** file through the **using** directive.

8. Press the F5 key to run the application.

9. Enter some text in the text box below the **Enter the text to be printed** label (Fig.C#-6.42).

10. Click the **Print** button, as shown in Fig.C#-6.42.

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_217_0.png)

The **Print** dialog box appears. In the **Print** dialog box, you can specify various options and preferences for printing the text. In this case, we have selected the **Current Page** radio button under the **Page Range** section and specified 2 as the **Number of copies** (Fig.C#-6.43).

11. Click the **Print** button in the **Print** dialog box to start printing the document, as shown in Fig.C#-6.43:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_217_1.png)

Finally, let’s recapitulate all the main points that you have learned in this chapter.

## Summary

In this chapter, you have learned how to:

- Create toolbars, menus, and status bar
- Work with dialog boxes

## Chapter 7

## Introducing Windows Presentation Foundation and XAML

In this Chapter:

- Explaining the WPF 4.0 Architecture
- Exploring the Improvements in WPF 4.0
- Describing Types of WPF Applications
- Exploring the WPF 4.0 Designer
- Exploring XAML and WPF
- Working with WPF 4.0 Controls
- Working with Resources and Styles

Apart from including Windows Forms to develop desktop applications, Visual Studio 2010 encompasses Windows Presentation Foundation (WPF), previously known as Avalon, which offers several features and functionalities to develop high-end desktop applications. WPF supports various media, such as text, images, audio, and video, and allows you to work with two-dimensional (2D) as well as three-dimensional (3D) graphics. Unlike Windows Forms, which require numerous technologies, such as Graphics Device Interface (GDI+), Windows Media Player, and DirectX application programming interfaces (APIs) to work with 2D, 3D, and multimedia, WPF offers a cohesive medium that inherently provides the functionality of these technologies. This implies that you do not need to separate APIs in WPF to work with graphics, animations, and multimedia, and therefore it is easier and simpler to develop graphic-rich desktop applications by using WPF.

WPF was initially incorporated with .NET Framework 3.0 and was fully included in .NET Framework 3.5 and Visual Studio 2008. The version of WPF included in .NET Framework 4.0 is WPF 4.0.

In this chapter, you learn about the architecture of WPF 4.0, the improvements and enhancements in WPF 4.0, and the different types of WPF 4.0 applications. In addition, you learn about the WPF 4.0 Designer, the use of Extensible Application Markup Language (XAML) in WPF, and some of the common and new controls of WPF 4.0. You also learn how to use resources and styles in WPF.

We start the chapter by discussing the architecture of WPF 4.0.

### Explaining the WPF 4.0 Architecture

Although WPF 4.0 is a part of .NET Framework 4.0, it has both managed and unmanaged components. The managed and unmanaged components of WPF 4.0 are shown in Fig.C#7.1:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_219_0.png)

Fig.C#7.1

As shown in Fig.C#7.1, WPF 4.0 consists of the PresentationFramework, PresentationCore, WindowsBase, Common Language Runtime (CLR), Media Integration Layer (MIL or milcore), User32, DirectX, and Kernel components. The components that are shaded, that is, PresentationFramework, PresentationCore, WindowsBase, and milcore, are those that are essential to work with WPF 4.0 applications. To ensure that there is tight integration with DirectX, milcore is written in unmanaged code.

> Note
> The CLR, WindowsCodecs, User32, DirectX, and Kernel components of WPF 4.0 are part of the Microsoft Windows Vista operating system and it is beyond the scope of this chapter to discuss them.

Now, let's briefly discuss the components of WPF 4.0 in detail.

### The PresentationFramework Component

The PresentationFramework component refers to the PresentationFramework.dll assembly in .NET Framework 4.0. This component offers classes to control the appearance and presentation of WPF 4.0 applications. For instance, controls, layout, and data binding in WPF applications are handled by the PresentationFramework component.

### The PresentationCore Component

The PresentationCore component is implemented as the PresentationCore.dll assembly in .NET Framework 4.0. This component provides some of the most commonly used types and features of WPF 4.0. The classes and types offered by the PresentationCore component provide certain essential functionalities, such as properties, and events in WPF 4.0. Note that the PresentationCore component does not offer types for the user interface (UI) of WPF 4.0 applications such as those offered by the PresentationFramework component.

### The WindowsBase Component

The WindowsBase component is implemented as the WindowsBase.dll assembly in .NET Framework 4.0. This component provides the fundamental features of WPF, such as threading. Some of these features can be accessed and used outside the WPF domain.

### The MIL or Milcore Component

WPF 4.0 also contains an unmanaged component called milcore. An unmanaged component in WPF 4.0, milcore interacts with DirectX and acts as a medium or interface between CLR and DirectX (and managed WPF components). Due to this interaction with DirectX, milcore enables the display of 2D as well as 3D content in WPF 4.0 applications.

Now, let's discuss the various improvements in WPF 4.0.

### Exploring the Improvements in WPF 4.0

WPF forms an essential component of the .NET Framework that enables .NET application developers to create WPF applications with visually appealing UIs. Using WPF 4.0, .NET developers can integrate 3D graphics, multimedia, animation, document support, speech recognition, and more into the applications. WPF 4.0 introduces a few improvements that include the following:

- **Addition of new controls:** Refers to the introduction of the new controls such as DataGrid, Calendar, and DatePicker. These controls enable application developers to create enhanced enterprise-level applications. In addition, these controls are 99% compatible with their Silverlight versions, which allow the reuse of code between Silverlight and WPF implementations.
- **Touch input and their manipulation:** Refers to the support for touch input that WPF 4.0 elements provide. The UIElement 3D, and ContentElement classes consist of events that are raised when a user touches an element on a touch-screen. You can manipulate the UIElement class by rotating, scaling or translating it. For instance, when you can view some photographs in an application, you are able to zoom, move, resize, or rotate the photograph on the computer screen.
- **New text rendering stack:** Refers to the improvements made in rendering text, which include text clarity, configurability, and support for international languages. Moreover, users can now select from auto, aliased, grayscale or ClearType text rendering modes. In addition to all this, the text stack includes support for the display-optimized character layout so that text with sharpness comparable to Win32/GDI text can be generated.
