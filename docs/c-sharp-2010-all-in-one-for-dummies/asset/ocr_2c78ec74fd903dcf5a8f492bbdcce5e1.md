# The Wrap Panel

The Wrap Panel automatically wraps overflow content onto the next line(s). This is different than how a typical toolbar works, where overflow items are hidden when there isn't enough real estate to show them. Figures 2-3 and 2-4 show the same content controls from the Stack Panel (a mixture of buttons and a text block) in a Wrap Panel. The first Window has enough room to show all the UIElements, and the second shows the wrapping of elements because of a lack of room. The XAML for the Wrap Panel sample is in Listing 2-3.

![](bbox=[0.05, 0.31, 0.52, 0.4])

![](bbox=[0.05, 0.43, 0.27, 0.52])

Note that even with the Wrap Panel, if the container can't hold the widest item (the last button in the example), some clipping will take place.

# Listing 2-3: Wrap Panel XAML

```
```xml
<WrapPanel>
    <Button Content="A Button"/>
    <Button Content="Another Button"/>
    <TextBlock Text="This is a text block"/>
    <Button Content="Short"/>
    <Button Content="Really Long Button Label"/>
</WrapPanel>
```
```

# The Dock Panel

The Dock Panel uses attached properties (introduced in Chapter 1 of this minibook) to “dock” child UIElements. (See Figure 2-5 and Listing 2-4.) An important thing to remember is that child elements are docked in XAML order, which means if you have two items assigned to the left side (through DockPanel.Dock="left"), the first UIElement as it appears in the XAML gets the far left wall of the Panel, followed by the next item.