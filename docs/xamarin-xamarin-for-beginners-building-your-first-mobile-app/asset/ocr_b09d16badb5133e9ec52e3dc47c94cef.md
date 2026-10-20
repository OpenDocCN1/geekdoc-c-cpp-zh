the previous three conversions. In this lesson from the series on learning Android application programming using Xamarin.Forms, we will talk about each of the three previous types and how to implement it in a simple practical example.

# Withdrawal Translation:

Withdrawal is the transition without changing the size of the body, or making any rotation. Any element of the VisualElement class is rotated by the TranslationX and TranslationY properties. When assigning a positive value to the TranslationX property, this will move the object horizontally to the right (relative to its current location). When assigning a positive value to the TranslationY property, this will move the object vertically downward (relative to its current position). Let's start by testing this type of conversion. Start by creating a new Blank App (Xamarin.Forms Portable) project named TransformsApp, then just keep the TransformsApp (Portable) and TransformsApp.Droid projects as we did in this lesson. Next we will add a content page based on the XAML code, as we have already done in this lesson, we will call it TranslationPage. Make sure the contents of this page are as follows:

```
<ContentPage xmlns = "http://xamarin.com/schemas/2014/forms" xmlns: x = "http://schemas.microsoft.com/winfxx/2009/xaml" x: Class = "TransformsApp.TranslationPage">
    <StackLayout Padding = "20, 10">
        <Frame x: Name = "frame" HorizontalOptions = "Center" VerticalOptions = "CenterAndExpand" OutlineColor = "Accent">
            <Label Text = "TEXT" FontSize = "Large" />
        </Frame>
        <Slider x: Name = "xSlider" Minimum = "- 200" Maximum = "200" Value = "{Binding Source = {x: Reference frame}, Path = TranslationX}" />
        <Label Text = "{Binding Source = {x: Reference xSlider}, Path = Value, StringFormat = 'TranslationX = {0: F0}'}" HorizontalTextAlignment =
```