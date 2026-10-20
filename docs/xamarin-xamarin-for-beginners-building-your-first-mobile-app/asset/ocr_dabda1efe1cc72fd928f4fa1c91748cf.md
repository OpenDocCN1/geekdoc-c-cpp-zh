images we get from the web. Except that we use the FromResource static function of the ImageSource class. In this section, we’ll discuss a practical application to browse through a set of images that I have created specifically for this purpose. You will be browsed by two buttons: "Next" and "Previous", in addition to a sticker showing a simple information about the current image number displayed on the image element. These images will be locally located within the app. Now let's start by creating a new app called ResourceImageApp of type Blank App (Xamarin.Forms Portable). Keep only the ResourceImageApp (Portable) and ResourceImageApp.Droid projects. Add a new content page named ContentImagePage and make sure the contents of the ResourceImagePage.cs file are as follows:

```
1using System;
2using Xamarin.Forms;
3
4namespace ResourceImageApp
5{
6  public class ResourceImagePage : ContentPage
7  {
8    private Button btnPrev;
9    private Button btnNext;
10    private Image resourceImage;
11    private Label lblInfo;
12    private int currentIndex = 1;
13
14    public ResourceImagePage()
15    {
16      lblInfo = new Label
17      {
18        VerticalOptions = LayoutOptions.Start,
19        HorizontalOptions = LayoutOptions.FillAndExpand,
20        HorizontalTextAlignment = TextAlignment.Center,
21        TextColor = Color.Accent,
22        FontSize = Device.GetNamedSize(NamedSize.Medium,
```