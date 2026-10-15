
## Summary

In this chapter, you have learned about Windows Forms and how to perform various actions on them, such as adding controls, disabling and enabling Windows Form, changing the title of Windows Form, setting the border of Windows Forms, and hiding and displaying the Maximize, Minimize and Close buttons of a Windows Form. Next, you have learned how to create multiple forms in a Windows application. Moreover, you have learned how set different properties of controls and forms. Finally, the chapter described how to handle mouse and keyboard events.

This chapter provided an overview of Windows Forms and their controls. The CD accompanying this book contains five bonus chapters that provide more detailed and in depth description of Windows Forms controls:

- Bonus Chapter 1 describes the Button, Label, TextBox, RichTextBox, and MaskedTextBox controls
- Bonus Chapter 2 describes the RadioButton, CheckBox, ListBox, CheckedListBox, and ComboBox controls
- Bonus Chapter 3 covers the ListView, TreeView, ImageList, PictureBox, Panel, GroupBox, and TabControl controls
- Bonus Chapter 4 elucidates the SplitContainer, ScrollBar, TrackBar, ToolTip, NotifyIcon, MonthCalendar, DateTimePicker, Timer, and ProgressBar controls
- Bonus Chapter 5 describes the ToolStrip, MenuStrip, ContextMenuStrip, StatusStrip, and Dialog Box controls

In the next chapter, you learn about the fundamentals of Windows Presentation Foundation (WPF).

## 9

## Introducing Windows Presentation Foundation

| If you need an Immediate Solution to: | See page: |
|---|---|
| Working with WPF Windows | 354 |
| Adding Rows and Columns to a Grid Through XAML | 359 |
| Creating a Dialog Box in a WPF 4.0 Application | 361 |
| Working with Custom Routed Events | 364 |

![](img/e073a4882197be4ab61103cbe0bcb394_340_0.png)

## In Depth

As of now, you have learned about the development of desktop applications by using Windows Forms. Visual Studio 2010 encompasses another technology, known as Windows Presentation Foundation (WPF), to develop desktop applications. WPF, previously known as Avalon, offers several features and functionalities to develop high-end desktop applications. It supports various media, such as text, images, audio, video and allows you to work with Two-Dimensional (2-D) as well as Three-Dimensional (3-D) graphics. As you know, Windows Forms require numerous technologies to work with 2-D, 3-D, and multimedia. Some examples of these technologies are: GDI+, Windows Media Player Application Programming Interfaces (APIs), and DirectX APIs. Unlike Windows Forms, WPF inherently provides these technologies, so that you do not need separate APIs in WPF to work with graphics, animations, and multimedia. Therefore, it is easier and simpler to develop graphic-rich desktop applications by using WPF. All the design-related elements in WPF applications are processed by DirectX.

Similar to Windows Forms, WPF is also suitable for both User Interface (UI) designers and application developers. It provides a convenient platform for designers and developers to share and collaborate their work to accomplish their task. WPF, initially incorporated with .NET Framework 3.0, is included in .NET Framework 3.5 and 4.0. The version of WPF included in .NET Framework 4.0 is WPF 4.0. WPF also supports Extensible Application Markup Language (XAML). XAML is a declarative markup language based on Extensible Markup Language (XML) introduced by Microsoft Corporation. This markup language allows designers to easily and quickly define and describe the elements for the UI of WPF applications. After that, application developers can use the UI elements defined with the help of XAML to specify the application logic in the code-behind files in any of the .NET languages, such as C#. In addition, you can also use the code-behind files to create UI elements at run time. Consequently, WPF allows both segregation and integration of the UI aspect and application logic in WPF applications.

In this chapter, you learn about the new features and essential concepts of WPF 4.0, such as its architecture, class hierarchy, and application model. The chapter also explains how to create and execute WPF 4.0 applications. In addition, this chapter describes the WPF 4.0 designer, basics of XAML, WPF properties and events, and WPF dialog boxes.

Let’s first discuss the new features of WPF 4.0.

## New Features of WPF 4.0

WPF is a UI framework, which helps you to create interactive client applications. It supports various application development features, such as controls, graphics, layout, and data binding. WPF uses XAML language for application programming. You can use WPF for creating both standalone and browser-hosted applications.

WPF 4.0 has several improvements and enhancements over its previous version, WPF 3.5. Some new features of WPF 4.0 include:

- New WPF controls to develop business applications
- Support for development of touch-enabled application
- Easing functions for enhancing animations
- Visual State Manager (VSM)
- Selection and Caret brushes
- New WPF text rendering stack
- Improvements in XAML Browser Applications (XBAPs)

Let’s explore these features of WPF 4.0 in detail.

## New WPF Controls

In WPF 4.0, three new controls: DataGrid, Calendar, and DatePicker, are added to develop business applications. These controls enable you to reuse application’s code and create rich client and Web applications. Let’s look at a brief description of these controls in the next sections.

## DataGrid

DataGrid is a control that displays the data from a database table in a grid format. It displays the data in the form of rows and columns. In addition, it generates columns automatically, on the basis of the type of the data stored in them, by setting the ItemsSource property. You can perform various operations, such as grouping, sorting, and filtering, on the data stored in the DataGrid control. Moreover, the DataGrid control enables you to perform validation on the cell and row levels. At the cell level validation, you can validate the properties of a bound data object (cell) when another user updates the value. However, at the row level validation, you can validate the entire data objects (rows) when another user modifies the data in a row.

> NOTE
> To learn more about the DataGrid control, refer Chapter 25, Data Binding in Windows Forms and WPF Applications.

## Calendar Control

Calendar is a control that enables you to select a date from a visual calendar. It can be used as a separate control or the drop-down part of the DatePicker control. Figure 9.1 shows the Calendar control in the MainWindow of a WPF application:

![](img/e073a4882197be4ab61103cbe0bcb394_342_0.png)

Figure 9.1: Displaying the Calendar Control in MainWindow

> NOTE
> To learn more about the Calendar control, refer Chapter 12-Using Graphics and Multimedia in Windows Forms and WPF.

## DatePicker

DatePicker is a control that enables you to select a date by either typing it into a text field or using a drop-down Calendar control. Figure 9.2 shows the DatePicker control in the MainWindow of a WPF application:

![](img/e073a4882197be4ab61103cbe0bcb394_342_1.png)

Figure 9.2: Displaying the DatePicker Control in MainWindow

![](img/e073a4882197be4ab61103cbe0bcb394_344_0.png)

## Figure 9.3: Displaying Different States of a Button Control

ControlTemplate is a class that is used to specify the visual structure and behavioral aspects of a control, so that these aspects can be shared across multiple instances of the control. The VisualStateManager class enables you to specify different states for a control and the appearance of a control.

## Selection and Caret Brushes

In WPF 4.0, two new brushes, Selection and Caret, are added to highlight the selected text and paint the cursor. These brushes work on input and reading controls, such as TextBox, RichTextBox, and FlowDocumentReader. These brushes are available in the form of the properties of the TextBoxBase class. These properties are as follows:

- SelectionBrush – Creates a brush to highlight the selected text
- CaretBrush – Creates a brush to paint the cursor

The TextBoxBase.SelectionBrush and TextBoxBase.CaretBrush properties belong to the System.Windows.Controls.Primitives namespace. The following is the syntax of these properties:

```
public Brush SelectionBrush { get; set; }
public Brush CaretBrush { get; set; }
```

The following code snippet shows an example of using SelectionBrush:

```
<TextBox SelectionBrush="Yellow" SelectionOpacity="0.8" Foreground="Green">
You are using the SelectionBrush and CaretBrush properties.
</TextBox>
```

The preceding code snippet creates a text box and adds the text, You are using the SelectionBrush and CaretBrush properties, to it. We have specified the SelectionBrush property as yellow. Note that there is another property, SelectionOpacity, which is set as 0.8 to customize the appearance of the selected text. Figure 9.4 shows the use of the SelectionBrush property:

![](img/e073a4882197be4ab61103cbe0bcb394_344_1.png)

## Figure 9.4: Displaying a Highlighted Text Using the SelectionBrush Property

The following code snippet shows an example of using the CaretBrush property:

```
<TextBox Foreground="Green" CaretBrush="Red">
You are using the SelectionBrush and CaretBrush properties.
</TextBox>
```

The preceding code snippet creates a text box and adds the text, You are using the SelectionBrush and CaretBrush properties, to it. We have specified the CaretBrush property as red and the Foreground property as green. Figure 9.5 shows the output of the CaretBrush property:

![](img/e073a4882197be4ab61103cbe0bcb394_344_2.png)

## Figure 9.5: Displaying a Red Color Cursor Using the CaretBrush Property

You can find the code to use the SelectionBrush and CaretBrush properties in the SelectionCaretBrushesUse application (available in the CD).
