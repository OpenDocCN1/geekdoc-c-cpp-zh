
```csharp
57     };
58
59     Content = new StackLayout
60     {
61         Children = {
62             lblInfo,
63             resourceImage,
64             buttonsLayout
65         }
66     };
67
68     Padding = new Thickness(5, 5, 5, 5);
69
70     UpdateScreen();
71     }
72
73     private void BtnPrev_Clicked(object sender, EventArgs e)
74     {
75         currentIndex--;
76         if (currentIndex == 1)
77         {
78             btnPrev.IsEnabled = false;
79         }
80
81         btnNext.IsEnabled = true;
82
83         UpdateScreen();
84     }
85
86     private void BtnNext_Clicked(object sender, EventArgs e)
87     {
88         currentIndex++;
89         if (currentIndex == 5)
90         {
91         btnNext.IsEnabled = false;
92     }
93
94     btnPrev.IsEnabled = true;
95
96     UpdateScreen();
97    }
98
99     private void UpdateScreen()
100    {
101      lblInfo.Text = string.Format("{0}", currentIndex);
102      string path = string.Format("ResourceImageApp.Images.res0{0}.jpg", currentIndex);
103      resourceImage.Source = ImageSource.FromResource(path);
104    }
105  }
106 }
```

Then navigate to the App.cs file and make sure that it looks like this:

```csharp
public App ()
{
    // The root page of your application
    MainPage = new ResourceImagePage ();
}
```

Right-click on the ResourceImageApp (Portable) joint project and choose Add, and from the side menu that appears choose New Folder. This will create a new folder within this project, called Images. Then right-click on the new Images folder and select Add. Choose image files: res01.jpg, res02.jpg, res03.jpg, res04.jpg, res05.jpg (click here to download Images.zip). The images in this order contain the words "Welcome to Hassoub Academy". Right-click again on each file name you just added to the project and from the menu select Properties. The file properties will appear; set the Build Action property to Embedded Resource as shown in the following figure:

![](img/affff2e3b09de80cc0ffe811bbf63f5d_69_0.png)

Once you click the Back button, the Next button will be back up. Let's discuss the operating code for this application. Note in lines 8 through 11 that I have declared special fields that represent most of the visual elements that we will deal with in this application: a picture element, a label element, and two buttons for the next and previous. In line 12, you declare a special variable currentIndex that represents the current file number that we would like to display in the image file and has an initial value of 1. The ResourceImagePage class structure configures all the visual elements used, as we know. In lines 16 through 23, we set the properties of the lblInfo label, where we assign the LayoutOptions.Start value to the VerticalOptions property so that it appears at the top of the screen. We also assigned the TextAlignment.Center value for the HorizontalTextAlignment property so that the text would appear horizontally. As for the resourceImage image element, we set its properties in lines 25 through 30, where we set the Aspect property value to Aspect.AspectFit to fill the image space available with respect to the proportion of the appearance of the image. Next comes the adjustment of the btnPrev (previous) and btnNext (next) buttons from lines 32 to 45. Later, we will add these buttons to their stacked layout, buttonsLayout, which is why we want to make these buttons adjacent horizontally and fill the horizontal space available to them. Note the LayoutOptions.FillAndExpand value for the HorizontalOptions property for both. We declare the StackLayout on lines 47 through 57. We will add to this layout the buttons btnPrev and btnNext and set the Orientation property to StackOrientation.Horizontal to show the previous and next buttons horizontally and not vertically. We will add this stack layout shortly to the basic stack layout of the page.

We set the content property of the page in lines 59 to 66 so that we create a new stack layout that contains the elements: label, image, and stack layout of buttons, respectively. This is why previous items appear in this order. Look at the following diagram showing the approximate position of the previous items on the page:

```
lblInfo

resourceImage

btnNext

btnPrev
```

The brown rectangle at the bottom represents the stack layout of buttonsLayout.

Finally, the UpdateScreen function (lines 99 to 104) updates the data that appears on the label and image elements at each click of the Next and Previous buttons. The FromResource function of the ImageSource class requires a text argument that represents the file ID. The file ID consists of the name of the application (or more precisely the Assembly) followed by a period, the name of the folder containing the image file, followed by another period, and finally the name of the file with its extension. In our example, the file ID for res01.jpg is as follows:

```
ResourceImageApp.Images.res01.jpg
```

The code of this app may look relatively large, but I assure you that you will write a few times in any commercial program that you can work on! This is due to the approach we have taken from the beginning of this series so far, relying on the code to create the entire user interface. Although it is possible to use good methods that contribute to the arrangement and organization of this code significantly, many developers prefer to use the other method in the development of applications using Xamarin.Forms, which is the use of XAML (code-like XML), which allows to separate the user interface from the software code. We will, of course, deal with this in future lessons.

## Conclusion

In this lesson we dealt with images in Xamarin.Forms. We discussed the issue from two different sides. The first aspect is to download the image from the Internet (and possibly from a local network), while the second aspect is to download the image from a local source. There is more to talk about in this topic, especially with regard to the acquisition of images through the sources of images associated with the device platform-specific or more precisely associated with the operating system running on the device, which is the Android system in our case. This is similar to the method used when working with image sources through Android Studio. We will cover this topic later in this book.

## Chapter VII

### Move between pages

Mobile apps typically consist of separate pages that the user navigates to take advantage of the capabilities the app offers. For Android apps, the Back button is essential in this navigation. In this tutorial from the Xamarin.Forms Android Application Programming Learning Series, we learn how to navigate between application pages. First we will talk about the concept of page navigation in a single application, and then we will talk about the types of content pages used in navigation through a simple practical example.

### The concept of navigating between application pages

Navigating between application pages is very similar to the principle on which a Stack works. The stack is known as a data structure that supports the concept of LIFO (Last In, First Out). When you move from page A to page B, page B is pushed to the top of the stack, resulting in it appearing to the user. Similarly, when you move from page B to page C, page C is pushed to the stack to be shown to the user. When we want to return to the original page A, page C is popped and removed from the stack, page B will be at the top of the stack (i.e. it will appear to the user), and page B will be removed from the stack and page A will be at the top of the stack. See the following figure to illustrate this idea:

![](img/affff2e3b09de80cc0ffe811bbf63f5d_74_0.png)

### Modal and Modeless Pages
