
```
public App ()
{
    // The root page of your application
    MainPage = new CounterPage ();
}
```

When you execute the program using F5, you will get a look similar to the following, I made several clicks on each of the buttons:

![](img/affff2e3b09de80cc0ffe811bbf63f5d_56_0.png)

As we know, images are essential elements of any application, they add aesthetic touch and give an explanatory impression of the basic functions of the application. We will continue our work in this series by explaining how to use images in Xamarin.Forms. Xamarin deals with bitmaps that may differ slightly for Android, iOS, and Windows, but if you rely on formats like JPEG, PNG and BMP, you won't have any problems.

Xamarin.Forms handles images in two main styles. The first method relies on platform-independent images, and the second method relies on platform-specific images or, more precisely, the operating system. You will address the first method in our lesson through two simple applications that illustrate this. The second method will be postponed to another lesson.

Images within Xamarin applications can be viewed by a visual element represented by the Image class. As with other visual elements that inherit from the VisualElement class, this element has many properties in common with any other visual element, such as the Label. In addition to other features that distinguish it, such as the Source property, which reflects the source of the image that will be displayed within it. This feature will be our focus in this lesson. Device independent images can be obtained in two different styles. In each method, you need to assign an object of the ImageSource class to the Image property of the Image object.

The first method is to get images directly from the Internet, by calling the

FromUri static function from the ImageSource class and passing the Uri address of the image file online.

The second method is to invoke the FromResource static function from the ImageSource class and pass the resource name to it. The following two simple applications will explain how to do this.

## Get a picture from the Internet:

Create a new app called WebImageApp of type Blank App (Xamarin.Forms Portable) and keep only the WebImageApp (Portable) and WebImageApp.Droid projects as we have already agreed. Add a new ContentPage as we did in this lesson. Name it WebImagePage and make sure that the contents of the WebImagePage.cs file are as follows:

```
using System;
using Xamarin.Forms;

namespace WebImageApp
{
    public class WebImagePage: ContentPage
    {
        public WebImagePage ()
        {
            Image webImage = new Image
            {
                VerticalOptions = LayoutOptions.FillAndExpand,
                HorizontalOptions = LayoutOptions.FillAndExpand,
                Source = ImageSource.FromUri (new Uri ("https://developer.xamarin.com/demo/IMG_2138.JPG?width=800")),
                Aspect = Aspect.AspectFit,
                BackgroundColor = Color.Accent
            };

            Content = new StackLayout
```
```
{
    Children = {
        webImage
    }
};
}
}
}
```

Then navigate to the App.cs file and make sure that it looks like this:

```
public App ()
{
    // The root page of your application
    MainPage = new WebImagePage ();
}
```

The application code is simple, it creates a new image object, assigns it to the webImage variable, and then makes that image object a child of the stack layout clearly.

What we are interested in now is the properties of the image object. The Source property is the source from which we get the image. In this application we will get the image from the Internet so we will use the static function ImageSource.FromUri that returns an object from the ImageSource row. Note that we've passed a new Uri object to this function:

```
ImageSource.FromUri (new Uri ("https://developer.xamarin.com/demo/IMG_2138.JPG?width=800"))
```

The address used here is:

```
"https://developer.xamarin.com/demo/IMG_2138.JPG?width=800"
```

Aspect specifies how the image is displayed within the Image element. They accept values from the Aspect of the same name. This number has three elements: AspectFit, AspectFill and Fill. In this application we used the AspectFit value which is the default value. Here's what the three previous values mean:

- * AspectFit: means that the image will appear within the element so that it is consistent with the space allocated to it, while respecting the aspect ratio of the image appearance.
- * AspectFill: In this case the image will appear within the element so that the aspect ratio of the image will be respected, but it will not take care of the space allocated to this element. Therefore, the image may appear truncated if it is larger than the element.
- * Fill: This value means that the image will appear to occupy the entire area allocated to the object without regard to the aspect ratio of the image. So just the image appears stretched horizontally or vertically. You have assigned Color.Accent to the BackgroundColor property of the image element in order to see the actual space occupied by that element. Run the previous program using F5 to get a look similar to the following, noting that I'm testing on a device with a 4.5-inch screen, so the results you get on your device may vary if you have a larger screen. If so, I recommend deleting the "? Width = 800" section of the image's Uri title from the Source property:

![](img/affff2e3b09de80cc0ffe811bbf63f5d_62_0.png)

Notice how the image appeared so that the space remained empty from the top and bottom. This is because it respected the aspect ratio of the original image. If you modify the Aspect property to carry the value Aspect.AspectFill, you will get a look similar to the following:

![](img/affff2e3b09de80cc0ffe811bbf63f5d_63_0.png)

Notice here how the image appeared slightly truncated. Now try the last case, assigning the value Aspect.Fill to the Aspect property to get a shape similar to the following:

![](img/affff2e3b09de80cc0ffe811bbf63f5d_64_0.png)

As expected, the image appeared to be stretched vertically because it would fill the entire space available for the image element without regard to the proportion of the appearance of the original image as noted.

## Get a picture from a local resource:

Working with images in this method is no different from the way we handle

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
```
typeof(Label))
23        };
24
25        resourceImage = new Image
26        {
27            VerticalOptions = LayoutOptions.FillAndExpand,
28            HorizontalOptions = LayoutOptions.FillAndExpand,
29            Aspect = Aspect.AspectFit
30        };
31
32        btnPrev = new Button
33        {
34            Text = "first",
35            HorizontalOptions = LayoutOptions.FillAndExpand,
36            IsEnabled = false
37        };
38        btnPrev.Clicked += BtnPrev_Clicked;
39
40        btnNext = new Button
41        {
42            Text = "next",
43            HorizontalOptions = LayoutOptions.FillAndExpand
44        };
45        btnNext.Clicked += BtnNext_Clicked;
46
47        StackLayout buttonsLayout = new StackLayout
48        {
49            Orientation = StackOrientation.Horizontal,
50            VerticalOptions = LayoutOptions.End,
51            HorizontalOptions = LayoutOptions.FillAndExpand,
52            Children =
53            {
54                btnNext,
55                btnPrev
56            }
```
