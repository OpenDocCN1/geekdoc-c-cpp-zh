
The storyboard lets you plot out exactly which elements will be moving, how fast they are moving, where they are moving, and so on.

The animations contained within a storyboard can be anything from simple animations that change one property from a source value to a target value to complex animations, such as key frame animations, where you indicate what a property’s value should be at specific time markers.

The animations I used in the preceding example are double animations, which animate a property of type double from a source value to a target value over a specific period of time.

## Migrating from Tab Bar Applications

In iOS applications, the tab bar control is an extremely common control that shows up in thousands of applications in the App Store. The purpose of this control is to segment an application into categories or provide quick, shortcut-style access to particular pieces of the application’s functionality. When there are more tabs than can be displayed on a single bar, a More button appears, which brings the user to a table view displaying the list of the remaining tabs. Tapping on any of the tabs launches the view controller associated with that particular tab.

Although Windows Phone 7 doesn’t have its own exact replica of the Tab Bar control, WP7 developers have plenty of options for building UIs that serve the same purpose as the Tab Bar control. These include the Pivot control, the Panorama control, and finally the Application Bar control. The following sections cover each of these controls respectively and how they support “tab bar-like” functionality.

## Using the Pivot Control

The Pivot control is an incredibly powerful control but also just as easy to use. A Pivot has a title and then a series of PivotItem child controls. Each of these PivotItem controls contains a XAML hierarchy of visual elements that can be anything from list boxes to buttons to whatever you like.

When the Pivot control first appears, the first pivot item is visible, and the title of the second pivot item is visible at the top of the Pivot control next to the first. Tapping the title of the second pivot item will pivot or slide the focus from the first pivot item to the second. This continues until you reach the last pivot item where the title of the first pivot item appears, allowing you to continuously move through the items without having to worry about using the back button.

One of the places you will see the Pivot control used extensively is Outlook for WP7. You can “pivot” between different views of your mail and, when used in your application, you can pivot between different categories of information or different areas of functionality within your application.

To see the Pivot control in action, you can make use of the ready-made Pivot Application WP7 template. Open up Visual Studio and create a new project. Choose the Pivot Application template and then run it. You should see a screen that looks like the one in Figure 9.3.

![](img/04a00d46bb1059867d95707babd62ee7_128_0.png)

Figure 9.3 Using the Pivot control.

Tap the word “second” to see the Pivot control slide so that the contents of the first pivot item move away and the contents of the second pivot item slide into view. Listing 9.3 shows the XAML for the Pivot control. As you can see, it is fairly straightforward, and the Pivot control is doing a great deal of work on your behalf.

### Listing 9.3 MainPage.xaml from the Pivot Control Application Template

```
<controls:Pivot Title="MY APPLICATION">
    <!--Pivot item one-->
    <controls:PivotItem Header="first">
        <!--Double line list with text wrapping-->
        <ListBox x:Name="FirstListBox" Margin="0,0,-12,0"
            ItemsSource="{Binding Items}">
            <ListBox.ItemTemplate>
                <DataTemplate>
                    <StackPanel Margin="0,0,0,17" Width="432">
```

```
<TextBlock Text="{Binding LineOne}"
    TextWrapping="Wrap"
    Style="{StaticResource PhoneTextExtraLargeStyle}"/>
    <TextBlock Text="{Binding LineTwo}"
    TextWrapping="Wrap" Margin="12,-6,12,0"
    Style="{StaticResource PhoneTextSubtleStyle}"/>
    </StackPanel>
    </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox>
</controls:PivotItem>
<!--Pivot item two-->
<controls:PivotItem Header="second">
    <!--Triple line list no text wrapping-->
    <ListBox x:Name="SecondListBox"
        Margin="0,0,-12,0" ItemsSource="{Binding Items}">
        <ListBox.ItemTemplate>
            <DataTemplate>
                <StackPanel Margin="0,0,0,17">
                    <TextBlock Text="{Binding LineOne}"
                    TextWrapping="NoWrap" Margin="12,0,0,0"
                    Style="{StaticResource PhoneTextExtraLargeStyle}"/>
                    <TextBlock Text="{Binding LineThree}"
                    TextWrapping="NoWrap" Margin="12,-6,0,0"
                    Style="{StaticResource PhoneTextSubtleStyle}"/>
                </StackPanel>
            </DataTemplate>
        </ListBox.ItemTemplate>
    </ListBox>
</controls:PivotItem>
</controls:Pivot>
```

It is surprisingly easy to use this control. Just create a new Pivot control and then define the panels through which you want your user to be able to pivot. Pivots can be used for everything from a complicated line of business applications to social applications, and even for casual gaming scenarios.

Experiment with this control and see what kinds of compelling UIs you can produce using just a Pivot control and the primitive Silverlight controls discussed in the previous chapter. You might be surprised by how much you can accomplish.

## Using a Panorama Application

Where the Pivot control slides items out of your way and new items into view atop a fixed background, the Panorama control is a much more fluid control. Rather than tapping the title of nearby items, you simply swipe to bring the nearby items into view. This creates a nice parallax scrolling effect where the user sees the background shift and the new items come into view.

In many cases you can use either a Panorama or a Pivot to provide the same functionality in your application; there are a few differentiating factors between the two controls. In a Pivot control, you tap the item names to bring the item content into view, and the Panorama requires a swiping gesture to bring the next item into view. The Pivot control is more often used when the UI structure of each element is somewhat similar to its peers. A Panorama control, as you can see when you flip through various hubs on a WP7 phone (especially the music area), gives the user a much looser, more fluid experience. You can use the Panorama to flip between data-driven views, rich graphical content, or anything else the phone provides.

The key differentiating factor to remember is that a Pivot control can be used to switch between completely unrelated areas of application functionality without it feeling awkward to the user. When using a Panorama control, users have the impression as they swipe that they are expanding the original view, perusing through more and more content all with a similar purpose or logical relation. This is why Panoramas are used for the “hub” UI pattern throughout the phone.

In other words, if you used a tab bar to separate completely disparate areas of functionality in your application, the Pivot control is the logical choice. On the other hand, if you used a tab bar to provide visual segmentation of logically related functionality, the Panorama is the natural choice for your UI.

To see the Panorama control in action, open up Visual Studio and create a new WP7 application, choosing the Panorama Application template. This will create a default implementation of a Panorama with a nice background image, a title, and two items that you can swipe between. Remember that if you swipe past the last item, the Panorama wraps around and the first item will come into view.

Figure 9.4 shows what it looks like when you run an application created by the stock Panorama Application project template.

Like the Pivot control, the Panorama control’s content is split up into separate child items, each one providing a piece of the virtual panorama experience. The code in Listing 9.4 shows the default XAML from the stock project template for the Panorama application.
