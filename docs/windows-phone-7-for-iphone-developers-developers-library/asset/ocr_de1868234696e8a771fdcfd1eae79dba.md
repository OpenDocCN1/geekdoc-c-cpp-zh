# Accepting Other Forms of User Input

Buttons and TextBoxes aren’t the only way users can interact with your application using out-of-the-box controls that come with the WP7 SDK. This next section introduces you to a few new controls that provide richer and more flexible ways of accepting input from the user, such as the following:

+   - Checkbox—There is no functional native UIKit control in iOS for a check box.
+   - RadioButton—A UISegmentedControl often provides similar functionality in iOS.
+   - PasswordBox—A UITextField control with the secureTextEntry property set to YES provides nearly identical functionality in iOS.
+   - Slider—A UISlider control provides this functionality in iOS, although iOS sliders are hard to customize and always appear horizontally, whereas WP7 sliders can be easily customized and can be displayed vertically without customization.
+   - HyperlinkButton—The easiest way to produce this functionality in iOS is to create a tappable label that has been styled to look like a hyperlink (for example, blue, underlined text).

Open up the MainPage.xaml file that we’ve been working with throughout this chapter and add the code from Listing 8.7 to the page below the controls from the previous samples. I’ve deleted a couple of unnecessary controls to make room for the new UI elements (shown in Figure 8.3).

# Listing 8.7 Adding New User Input Elements

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