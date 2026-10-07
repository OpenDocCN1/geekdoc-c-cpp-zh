```
FontSize="StaticResource btnFontSize"
FontWeight="StaticResource btnFontWeight"
BitmapEffect="StaticResource btnTextImageEffect"
Text="StaticResource btnText0"
/>
<Grid>
```

Although resources make it easier to modify all of the buttons' appearance, they may make the code long and confusing. Because all of the buttons have the same basic appearance, the code contains a lot of redundancy, with each `Button`'s code repeating the Width, Height, Margin, Fill, and other properties.

A style gathers property values that be set as a group. It begins with a Style element contained in a resource dictionary. You can place the Style in any resource dictionary depending on how widely you want it to be available. For example, if you want a Style to be visible to the entire project, place it in the `Application.Resources` section of the App.xaml file; if you want the Style visible over a control, place it in the `Window.Resources` section; if you want it to be visible only to controls inside a `StackPanel`, place it inside the `StackPanel.Resources` section.

# STYLE SCOPE

Suppose you have a Grid that contains a group of Labels. You could use a style defined in `Window.Resources` to give them a similar appearance but might cause problems if you want to give other Labels in a different Grid a different appearance. In that case, you would have to define multiple styles (named and unnamed styles are described shortly), which will complicate the code.

It's better to give Styles the most limited scope possible while still doing the job. That keeps the styles where they are used and lets you use unnamed styles to simplify your code.

A style can have an `x:Key` attribute to give it a name and a `TargetType` attribute to indicate the kind of control to it should apply. (The next section says more about these attributes.)

Inside the Style element, `Setter` and `EventSetter` define the style's property values and event handlers, respectively.

A `Setter` sets a property's value. It takes two attributes—Property and Value—that give the property to be set and the value it should hold. The Property Value can be a simple value like Red or 7, or it can be an element attribute specifying something more like a brush. (EventSetters are described later in this chapter.)

The RedRectangles example program uses the following code to define a Style named RedRectStyle that applies to Rectangles. The Stroke, StrokeThickness, Width, Height, and Margin setters use