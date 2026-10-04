Currently, the Planet Wrox website doesn't benefit a whole lot from changing the client IDs for any of the existing controls, so there's no need to change any right now. However, in later chapters, use the ClientIDMode property to create cleaner client IDs.

Although the current banner control makes easy to display a banner at various locations in your site, it isn't very smart. All it can do is display a linked image and that's it. To improve its usability, you can add behavior to the control so it can behave differently on different pages in your site.

# ADDING LOGIC TO YOUR CONTROLS

Although using controls for repeating content is quite useful, they become even more useful when you add custom logic to them. By adding public properties or methods to a user control, you can influence its behavior at runtime. When you add a property to a user control, it becomes automatically available in IntelliSense and in the Properties Grid for the control you are working with, making it easy to change the behavior from another file like a page.

To add properties or methods to a user control, you add them to the Code Behind of control. In its simplest form, a property looks exactly like the properties you see in Chapter 5. For more advanced scenarios you need to add View State properties, which are able to maintain their state across postbacks. In the next two exercises you will see how to create these types of properties.

# Creating Your Own Data Types for Properties

To make the banner control more useful, you can add a second image to it that displays a horizontal banner. You could also add a property to the control that determines whether to display the vertical or horizontal image. You could do this by creating a numeric property of type System.Byte. 0 would be vertical and 1 would be horizontal, for example. However, this makes it hard to remember what each number represents. You can make it a bit easier by creating a String property that accepts the values Horizontal and Vertical. However, strings cannot be checked at compile time, so you might end up making a mistake, resulting in an error or in the incorrect banner being displayed. The .NET Framework supplies a nice way to solve this by enabling you to create your own data type in the form of an enumeration. With an enumeration, or enum for short, you assign numbers to human-text strings. Developers then use this readable text, while under the hood the numeric value is used. The following snippet shows a basic example of an enum (notice how the VB example does not use commas, whereas they are required in C#):

```
VB.NET
Public Enum Direction
Horizontal
Vertical
End Enum
```

```
C#npublic enum Direction
{
    Horizontal,
    Vertical
}
```