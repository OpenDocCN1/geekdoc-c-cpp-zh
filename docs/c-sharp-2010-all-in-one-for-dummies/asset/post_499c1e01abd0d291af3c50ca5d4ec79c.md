
## Chapter 2: Understanding the Basics of WPF

### In This Chapter

- Laying out applications
- Using layout panels
- Working with the grid
- Implementing display-only, input, and list-based controls

As Chapter 1 explains, WPF brings not only a dramatic shift to the look and feel of Windows applications but also changes the manner of development. The days of dragging and dropping controls from the toolbox onto a form are long gone. Even though it is still possible to drag and drop in WPF, you will find yourself better off and much happier if you work in XAML directly.

What was once difficult is now relatively simple. For example, in traditional Windows applications, when the user changes the size of the form, the controls typically stay huddled in their corner and a large area of empty canvas is displayed. The only cure for this was a lot of custom code or expensive third-party controls. WPF brings the concept of flow layout from the Web into the Windows world.

In the GDI/GDI+ world of WinForms, modifying a control's style or building complex looks was a Herculean feat. WPF has completely redefined the control paradigm, giving you, the developer, the freedom to make a control do unimaginable tasks — including playing a video on a button face. However, keep in mind that just because you can do something doesn't mean you should!

In this chapter, we work with WPF's layout process to control the layout of your application and introduce you to the various WPF controls.

### Using WPF to Lay Out Your Application

Traditional Windows Forms development deals in absolutes. Position and size for controls are decided at design time and are based on the resolution of the developer's machine. When applications are deployed to users, the form that looked great on the developer's machine could now look very different (and possibly be downright unusable) because of hardware resolution differences.

### New tech, new terms

It seems every time Microsoft introduces a new technology, we have to learn a whole new set of terms. WPF is no different! At the root of the change are what we referred to as Forms and Controls in Windows Forms (WinForms). Here are some of the new terms:

- A *Form* in WinForms is referred to as a *Window* in WPF.
- Anything placed on a WinForms Form is called a *control*, whereas items placed on a WPF Window are referred to as *UIElements*.
- *Panels* are WPF UIElements used for layout.
- A *Control* in WPF is a UIElement that can receive focus and respond to user events.
- A *Content* control in WPF can contain only a single item, which can in turn be other UIElements.
- The WPF *Window* class is a specialized Content control.

Instead of depending on screen resolution, WPF measures UI Elements in Device Independent Units (DIUs) that are based on the *system DPI*. This enables a consistent look between many different hardware configurations.

WPF layout is based on *relative* values and is adjusted at runtime. When you place controls in a layout container (see the next section), the rendering engine considers the height and width only as "*suggested*" values. Location is defined in relation to other controls or the container. Actual rendering is a two-step process that starts with measuring all controls (and querying them for their preferred dimensions) and then arranging them accordingly. If controls could speak, the conversation might go something like this:

> > Layout Engine: "Control, how much space would you like to have?"
> > *<This is the Measure Stage>*
> > Control: "I would like 50 DIUs for height, 100 DIUs for width, and a margin of 3 DIUs in the containing Grid cell."
> > Layout Engine asks all other controls and layout containers.
> > Layout Engine: "Sorry, you can have only 40 DIUs for height, but I can grant the rest of your requests."
> > *<This is the Arrange Stage>*

## Arranging Elements with Layout Panels

Designing a Window begins with a Layout control, or Panel. Panels are different than Content controls in that they can hold multiple items, and depending on the Panel, a significant amount of plumbing is taken care of for you.

Panels control how UIElements relate to each other and to their containing UIElement and do not dictate absolute positioning. Most application Windows require some combination of Panels to achieve the required user interface. So it’s important to understand them all. WPF ships with six core Panels:

- Stack Panel
- Wrap Panel
- Dock Panel
- Canvas
- Uniform Grid
- Grid

### The Stack Panel

Stack Panels place UIElements in — wait for it — stacks. Items are placed in either a vertical pile (the default), like a stack of DVDs, or a horizontal arrangement, like books on a shelf. It is important to understand that the order items appear in the XAML is the order they appear in the Panel — the first UIElement in the XAML appears at the top (vertical) or on the far left (horizontal). Figures 2-1 and 2-2 show the same set of buttons in both orientations. Listing 2-1 contains the XAML for the Vertical Stack Panel shown in Figure 2-1.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_582_0.png)

The code for these samples can be found at csharpfordummies.net.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_582_1.png)

Figure 2-1: Vertical Stack Panel.

Book V Chapter 2 Understanding the Basics of WPF

### Listing 2-1: Vertical Stack Panel XAML

```
<StackPanel Name="pnlStack" Grid.Row="0"
    Orientation="Vertical">
    <Button Content="A Button"/>
    <Button Content="Another Button"/>
    <TextBlock Text="This is a text block"/>
    <Button Content="Short"/>
    <Button Content="Really Long Button Label"/>
</StackPanel>
```

### Figure 2-2: Horizontal Stack Panel.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_583_0.png)

Remember the conversation between the rendering Engine and the Control at the beginning of this chapter? The horizontal layout illustrates the clipping that can take place when the sum of the preferred sizes of controls in a container is larger than the container can hold.

Orientation (as well as all other properties) can be changed at runtime, as illustrated by Listing 2-2. The Button at the bottom of the Window changes the orientation, the button label, and the Window Title in the click event. Chapter 4 shows a better way of coding Button click events.

### Listing 2-2: Changing Stack Panel Orientation in Code

```
private void cmdOrientation_Click(object sender,
    RoutedEventArgs e)
{
    Button button = sender as Button;
    if (button.Content.ToString() == "Set Vertical")
    {
        pnlStack.Orientation = Orientation.Vertical;
        button.Content = "Set Horizontal";
        Title = "Stack Panel - Vertical";
    }
    else
    {
        pnlStack.Orientation = Orientation.Horizontal;
        button.Content = "Set Vertical";
        Title = "Stack Panel - Horizontal";
    }
}
```

### The Wrap Panel

The Wrap Panel automatically wraps overflow content onto the next line(s). This is different than how a typical toolbar works, where overflow items are hidden when there isn't enough real estate to show them. Figures 2-3 and 2-4 show the same content controls from the Stack Panel (a mixture of buttons and a text block) in a Wrap Panel. The first Window has enough room to show all the UIElements, and the second shows the wrapping of elements because of a lack of room. The XAML for the Wrap Panel sample is in Listing 2-3.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_584_0.png)

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_584_1.png)

Note that even with the Wrap Panel, if the container can't hold the widest item (the last button in the example), some clipping will take place.

### Listing 2-3: Wrap Panel XAML

```xml
<WrapPanel>
    <Button Content="A Button"/>
    <Button Content="Another Button"/>
    <TextBlock Text="This is a text block"/>
    <Button Content="Short"/>
    <Button Content="Really Long Button Label"/>
</WrapPanel>
```

### The Dock Panel

The Dock Panel uses attached properties (introduced in Chapter 1 of this minibook) to “dock” child UIElements. (See Figure 2-5 and Listing 2-4.) An important thing to remember is that child elements are docked in XAML order, which means if you have two items assigned to the left side (through DockPanel.Dock="left"), the first UIElement as it appears in the XAML gets the far left wall of the Panel, followed by the next item.
