Note that I dropped the lblMain variable because we assigned the Label object directly to the Content property.

# *Additional advantages over the app:*

You will notice from the previous application that the sticker appears in the upper left corner of the window. We'll make it appear in the center of the screen. Two adjective properties should be set for this purpose:
HorizontalOptions (for horizontal alignment options) and VerticalOptions (for vertical alignment options). Both of these properties are of type LayoutOptions, a struct structure that exists within the domain name Xamarin.Forms. This structure contains several ready-made fields that are useful for horizontal and vertical positioning options for the adhesion, which are very important options as we will see later in this series. Let us now make the required modification to the label within the MainPage class builder. The contents of the MainPage.cs file will look like this:

```
using Xamarin.Forms;

namespace SimpleTextApp
{
class MainPage: ContentPage
{
public MainPage ()
{
this.Content = new Label {
Text = "Welcome to Hsoub Academy!",
HorizontalOptions = LayoutOptions.Center,
VerticalOptions = LayoutOptions.Center
};
}
}
}
```