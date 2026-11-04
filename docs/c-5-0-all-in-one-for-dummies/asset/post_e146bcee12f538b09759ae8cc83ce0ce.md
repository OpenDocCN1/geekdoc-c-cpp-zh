
label; in this case, you use the Application Resource that you defined in the preceding section by retrieving it using its key value, which is Purpose. The label text is rendered with a font size of 25 units and is to be located in the grid in the first row and first column.

WOW! That line of XAML really packs quite the punch! Here's some of what is going on in there:

- **x:Name:** This attribute assigns a variable name to the object being created by the XAML tag. This enables you to access the object from the code-behind file. In this case, the variable name of the label object being instantiated is `lblPurpose`.
- **Content:** The value assigned to this attribute can be of any type. By default, you can assign it a `string` value, and it will render as you would think a standard label would render. In the WPF reality, `Content` can be composed of anything: a string, an image, an instance of a user control, a text box, and so on. For more info, see Chapter 2 of this minibook.
- **FontSize:** The size of the font of the label. It is important to note that the size isn't denoted in points; it's expressed in Device Independent Units. WPF gets away from the concepts of pixels and points and moves to a universal sizing strategy. Think of Device Independent Units as more of a ratio than a pixel. For instance, if the containing element of the label were 100 units by 100 units, the label would render as ½ of that size.
- **Grid.Row:** Identifies the grid row in which to render the label. Grid row collections are zero-based, meaning the first row is row 0, the second row is row 1, and so on. You should also note that the Label class doesn't contain a property named Grid. What you see here is the concept of attached properties. Attached properties are a way to assign the context of a current control relative to the properties of an ancestor control. In this case, you assign the label to appear in the first row (row index 0) of its containing grid. Also observe that the label is located within the `Grid` tags; this is how the ancestor `Grid` element is located.
- **Grid.Column:** Similar to `Grid.Row`, this attached property identifies the grid column in which to render the label. Together with `Grid.Row`, both properties identify the cell where the label is located. In this case, you assign the label to render in the first column of its containing grid. Grid column collections are also zero-based.

Go ahead and run your application. You now see Hello World displayed in the label on your Window. Congratulations, you have just created your first WPF application!

The complete solution is available at http://csharpfordummies.net in the chapter downloads.

![](img/80ff26f06fc9ab951e1cd4257b867366_599_0.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_599_1.png)

## Whatever XAML Can Do, C# Can Do Better!

Anything that you can implement using XAML can be implemented in C#. This is not true in reverse; not everything you can do in C# can be done in XAML. C# is the obvious choice for performing business logic tasks with procedural code that can't be expressed in XAML. In the following steps, you create an identical WPF application to the one you created in the preceding section, this time using C# to implement its functionality:

1. Create a new project by choosing File ▸ New Project.
2. Under Visual C#, select Windows.
3. Select WPF Application.
4. Name the application MyFirstCodeOnlyWPFApplication.
5. Click OK.
6. Open App.xaml.cs.
7. Override the OnStartup method to include the creation of the Purpose application resource by adding the following code to the App class:

```csharp
protected override void OnStartup(StartupEventArgs e)
{
    //create and add the Purpose application resource
    string purpose = "Hello WPF World. in C#";
    this.Resources.Add("Purpose", purpose);

    base.OnStartup(e);
}
```

8. Open MainWindow.xaml and give the Grid element a name by adding the following attribute:

```xml
x:Name="gridLayout"
```

9. Open MainWindow.xaml.cs, and in the default constructor, after the InitializeComponent method call, add the following code:

```csharp
//define grid column and row
this.gridLayout.ColumnDefinitions.Add(new ColumnDefinition());
this.gridLayout.RowDefinitions.Add(new RowDefinition());

//obtain label content from the application resource, Purpose
string purpose = this.TryFindResource("Purpose") as string;
Label lblPurpose = new Label();
lblPurpose.Content = purpose;
lblPurpose.FontSize = 25;

//add label to the grid
this.gridLayout.Children.Add(lblPurpose);

//assign attached property values
Grid.SetColumn(lblPurpose, 0);
Grid.SetRow(lblPurpose, 0);
```

Run the application and observe the resulting product is similar to that obtained in the section "Diving In! Creating Your First WPF Application," earlier in this chapter.

![](img/80ff26f06fc9ab951e1cd4257b867366_601_0.png)

The complete solution is available at the http://csharpfordummies.net website chapter downloads.

## Chapter 2: Understanding the Basics of WPF

### In This Chapter

- Laying out applications
- Using layout panels
- Working with the grid
- Implementing display-only, input, and list-based controls

As Chapter 1 explains, WPF brings not only a dramatic shift to the look and feel of Windows applications but also changes the manner of development. The days of dragging and dropping controls from the toolbox onto a form are long gone. Even though it is still possible to drag and drop in WPF, you will find yourself better off and much happier if you work in XAML directly.

What was once difficult is now relatively simple. For example, in traditional Windows applications, when the user changes the size of the form, the controls typically stay huddled in their corner and a large area of empty canvas is displayed. The only cure for this was a lot of custom code or expensive third-party controls. WPF brings the concept of flow layout from the web into the Windows world.

In the GDI/GDI+ world of WinForms, modifying a control’s style or building complex looks was a Herculean feat. WPF has completely redefined the control paradigm, giving you, the developer, the freedom to make a control do unimaginable tasks — including playing a video on a button face. However, keep in mind that just because you can do something doesn’t mean you should!

In this chapter, we work with WPF’s layout process to control the layout of your application and introduce you to the various WPF controls.

### Using WPF to Lay Out Your Application

Traditional Windows Forms development deals in absolutes. Position and size for controls are decided at design time and are based on the resolution of the developer’s machine. When applications are deployed to users, the form that looked great on the developer’s machine could now look very different (and possibly be downright unusable) because of hardware resolution differences.

Instead of depending on screen resolution, WPF measures UI Elements in Device Independent Units (DIUs) that are based on the *system DPI*. This enables a consistent look between many different hardware configurations.

WPF layout is based on *relative* values and is adjusted at runtime. When you place controls in a layout container (see the next section), the rendering engine considers the height and width only as “suggested” values. Location is defined in relation to other controls or the container. Actual rendering is a two-step process that starts with measuring all controls (and querying them for their preferred dimensions) and then arranging them accordingly. If controls could speak, the conversation might go something like this:

Layout Engine: “Control, how much space would you like to have?”

*<This is the Measure Stage>*

Control: “I would like 50 DIUs for height, 100 DIUs for width, and a margin of 3 DIUs in the containing Grid cell.”

*Layout Engine asks all other controls and layout containers.*

Layout Engine: “Sorry, you can have only 40 DIUs for height, but I can grant the rest of your requests.”

*<This is the Arrange Stage>*

### New tech, new terms

It seems every time Microsoft introduces a new technology, we have to learn a whole new set of terms. WPF is no different! At the root of the change are what we referred to as Forms and Controls in Windows Forms (WinForms). Here are some of the new terms:

- A *Form* in WinForms is referred to as a *Window* in WPF.
- Anything placed on a WinForms Form is called a *control*, whereas items placed on a WPF Window are referred to as *UIElements*.
- *Panels* are WPF UIElements used for layout.
- A *Control* in WPF is a UIElement that can receive focus and respond to user events.
- A *Content* control in WPF can contain only a single item, which can in turn be other UIElements.
- The WPF Window class is a specialized Content control.
