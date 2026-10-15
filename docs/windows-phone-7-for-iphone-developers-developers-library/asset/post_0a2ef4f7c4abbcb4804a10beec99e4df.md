
## Accepting Other Forms of User Input

Buttons and TextBoxes aren’t the only way users can interact with your application using out-of-the-box controls that come with the WP7 SDK. This next section introduces you to a few new controls that provide richer and more flexible ways of accepting input from the user, such as the following:

- Checkbox—There is no functional native UIKit control in iOS for a check box.
- RadioButton—A UISegmentedControl often provides similar functionality in iOS.
- PasswordBox—A UITextField control with the secureTextEntry property set to YES provides nearly identical functionality in iOS.
- Slider—A UISlider control provides this functionality in iOS, although iOS sliders are hard to customize and always appear horizontally, whereas WP7 sliders can be easily customized and can be displayed vertically without customization.
- HyperlinkButton—The easiest way to produce this functionality in iOS is to create a tappable label that has been styled to look like a hyperlink (for example, blue, underlined text).

Open up the MainPage.xaml file that we’ve been working with throughout this chapter and add the code from Listing 8.7 to the page below the controls from the previous samples. I’ve deleted a couple of unnecessary controls to make room for the new UI elements (shown in Figure 8.3).

### Listing 8.7 Adding New User Input Elements

```
<CheckBox x:Name="checkBoxOne" />
<RadioButton x:Name="ChoiceOne" GroupName="DefaultGroup">
    <TextBlock Text="Radio One" />
</RadioButton>
<RadioButton GroupName="DefaultGroup">
    <TextBlock Text="Radio Two" />
</RadioButton>
<Slider x:Name="SliderOne" Minimum="0" Maximum="100" Value="20" />
<HyperlinkButton x:Name="hyperLinkButtonOne" Click="hyperLinkButtonOne_Click" Content="hyperlink!!" />
<PasswordBox x:Name="PasswordBox" />
```

The first control added is a check box, and these are pretty simple. They let users specify Boolean values, such as whether they want to enable a specific preference or whether a particular statement about some data is true.

The next controls added were two radio buttons. These allow a user to select between a finite set of available options. When a user selects one radio button in a group, the state of all the other buttons is cleared. To indicate which buttons belong to the same group, just assign them the same string for the GroupName property. In the preceding code we assigned the GroupName property of the two radio buttons the value of DefaultGroup.

You can have as many radio button groups on a screen at a time as you can fit (or as your sense of good taste and design might allow).

Next we added a slider, which allows a user to “slide” a value indicator between some arbitrary minimum and maximum. You can use a slider control to prompt the user to pick a volume level, allocate resources to a particular object in a strategy game, or even choose how much of something the user might want to buy. Despite its simplicity, the slider is a powerful and versatile control that can be used in a variety of situations.

Next is the HyperlinkButton. As its name implies, this control presents the user with some text that resembles a standard browser-clickable hyperlink. When the link is tapped, it can either navigate the user to a particular page (a Silverlight page, not a web page) using the NavigateUri property, or you can perform custom logic in the Click event.

Last, we have the PasswordBox control. This control functions identically to a TextBox control except that a moment after each character is typed into the box, it is replaced with a dot. This pattern and style should be familiar to users of web browsers, iPhones, and many other mobile devices, and users should have no problem recognizing the purpose of this control. However, don’t mistake this control for built-in security. All this control does is obscure the display of the password; your code can still access the contents of this TextBox, and there is no automatic encryption. You will have to code your own security for passwords. Some tips and techniques for securing your WP7 application will be covered later in the book.

![](img/04a00d46bb1059867d95707babd62ee7_104_0.png)

Figure 8.3 Some more user input elements.

## Displaying Images

One of the easiest ways to spice up your application is through the use of images. Small, subtle images used judiciously throughout a UI, or even big images in the middle of a UI, can add a lot to your application and can often be the factor that sets your application above your competitors.

To use an image in iOS, developers typically use the UIImageView class. This class is derived from UIView and its sole purpose is for the display of images. Likewise, Windows Phone 7 developers have access to the Silverlight Image control, which is extremely easy to use both programmatically and through XAML markup.

The following code shows a basic image control configured completely through XAML.

```
<Grid x:Name="myGrid" Width="150" Height="150" Background="White">
    <Image x:Name="myImage"
        Source="/images/SuperAwesomeScreen.jpg" Stretch="Fill" />
</Grid>
```

Don’t worry about the Grid element; we’ll be getting to that shortly. In the preceding code, the image control is configured to display a JPEG image called SuperAwesomeScreen.jpg with a Fill stretch mode.

The stretch mode of an image can be set to None, Fill, Uniform, or UniformToFill. No stretch means the image will be displayed exactly as it appears in the file. A stretch mode of Fill means that the image will be expanded to fill whatever layout container it resides within. In the preceding code the parent grid is 150x150, so the image will be scaled up to that size, regardless of whatever size it might be in its original file form. When using the Fill mode, the aspect ratio of the image is not maintained, so it can often warp the original image. To maintain the ratio between height and width even after scaling, use the Uniform stretch mode. This mode will stretch the image as close as it can get to the new size while still keeping the original aspect ratio. Finally, the UniformToFill stretch mode is like Uniform, except it has permission to cut some of the image away to get a better fit within the parent container. In addition to the Stretch property, you can control a variety of other aspects of the image, such as the Width, Height, and Clip, which can be used to give images a nonrectangular shape.

Add the following Image element above the first TextBlock control within the StackPanel in the same MainPage.xaml file that we have been working with throughout this chapter.

```
<Image x:Name="sampleImage" />
```

That’s it. The default mode for the Stretch property is Uniform, which is good enough for our purposes. Now go into the code-behind for the XAML and change the implementation of the hyperlink button’s Click event to the following:

```
private void hyperLinkButtonOne_Click(object sender, RoutedEventArgs e)
{
    sampleImage.Source = new BitmapImage(
        new Uri("success.jpg", UriKind.RelativeOrAbsolute));
}
```

When this code executes, it is going to tell the Image control that it has a new source. This will cause the Image control to immediately redraw itself based on the new contents. The success.jpg file is included with the sample code that accompanies this chapter and can be seen in Figure 8.4.

Although this example might seem trivial, it is just the tip of the iceberg when it comes to the things that you can do with images. Knowing that the source and other properties of an image can be completely changed at runtime paves the way for all kinds of great functionality, such as downloading and caching images from the Internet or your application server, or even creating images on the fly, displaying them, and uploading them to an application server. Just about the only limitation on what you can do with images is your imagination.

![](img/04a00d46bb1059867d95707babd62ee7_106_0.png)

Figure 8.4 Using an Image control.

## Using a Basic List Box

So far we’ve been dealing with controls that deal with a single piece of information, such as a single image, an individual text box, or a single button. The list box control gives us the capability to define templates that will be used to render a list of items. This control comes built in with the capability to scroll through the items (including displaying a
