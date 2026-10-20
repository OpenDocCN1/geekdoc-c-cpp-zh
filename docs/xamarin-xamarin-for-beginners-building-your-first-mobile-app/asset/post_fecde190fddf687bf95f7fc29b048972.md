
## How Xamarin works

For iOS applications, Xamarin's C-Sharp translator translates the code into MSIL, and then Apple's Mac translator is used to generate native code running on iOS as if it were an Objective-C application.

For Android applications, the compiler will also generate the MSIL language, which in this case will create a common CLR for Android. The resulting applications in this case will also be very similar to those created using the Java language and Android Studio development environment for Android.

Finally, for apps running on Windows Phone and Windows 10 Mobile, apps are clearly supported, and will work like native apps created with Visual Studio without Xamarin.

## Conclusion

The Xamarin platform is promising, and has a long history and rich experiences before Xamarin emerged. Microsoft may have realized its importance, and the acquisition was completed. I recommend that you take the initiative to learn Xamarin, especially if you are a C Sharp programmer, or have preliminary information about it. The coming days may bring more support and surprises to the Xamarin platform, the first of which was to make it free for personal use or small software teams. Starting with the next lesson in this tutorial, we will install Visual Studio 2015 and start working with Xamarin.

## Chapter One

## Application architecture

### The structure of the application created using Xamarin

Run Visual Studio 2015, and after the main window appears go to the File menu and then to New and choose from the submenu that will appear Project option. As we did in the previous lesson, choose from the left side of the window that appears Cross-Platform, then choose Blank App (Xamarin.Forms Portable) from the middle section of the window. Give this project the name SimpleTextApp and click the OK button.

We will build a simple application that shows how to use a single Label to show text in Xamarin-based applications. From the Solution Explorer, which is usually on the right side of the Visual Studio development environment window, just keep the SimpleTextApp.Droid and SimpleTextApp (Portable) projects because we will only handle Android applications (as we agreed from the previous lesson). You get a shape similar to the following:

![](img/affff2e3b09de80cc0ffe811bbf63f5d_13_0.png)

SimpleTextApp (Portable) contains most of the code, which is common behavior in PCL-style projects. The code within the project (with the Portable section plus its name) is common to all types of applications running on any operating system including Android. The basic .cs that will be present in any Xamarin application we talked about in the previous lesson and saw how it contains the App class that inherits from the Application class, and how the builder of that class is responsible for creating the application's home page. You will notice that there are several libraries that interest us These include: Xamarin.Forms.Core, Xamarin.Forms.Platform, Xamarin.Forms.Xaml These

are the main libraries that are formed for Xamarin.Forms.

The SimpleTextApp.Droid project contains two folders: Assets and Resources. The Resources folder contains image files, layouts descriptions, and other files that are the resources for your app. Publish the Resources folder to see its structure. As for the Assets folder, the other public files that you want to include with your application are included. This project also contains the MainActivity.cs file, which contains a category with the same name as MainActivity, which is the main activity of the Android application. Open this file to find that this class contains the OnCreate function that is executed when you start the Android app. Note the following code statement within this function:

```
LoadApplication (new App ());
```

Obviously, it creates a new object from the App class within the SimpleTextApp (Portable) project and then passes it directly to the LoadApplication function to load the application and show it to the user. Creating a new object from the App class executes its structure and is responsible for creating the main page of the application as we have mentioned, however the idea will be well clarified after we start writing the code.

## Write code

Right-click on SimpleTextApp (Portable) in the Solution Explorer to display a context menu, choose Add and then from the submenu Choose Class. The window for adding a new class will appear. Visual Studio will add a new file to the project named MainPage.cs that contains a class with the same name and content similar to the following:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
```

```
namespace SimpleTextApp
{
class MainPage
{
}
}
```

We do not need most of the name ranges in the previous code in this program, we will currently need the domain name Xamarin.Forms. We will make the MainPage class inherit from the ContentPage class and add the builder to it. Modify the previous code to read as follows:

```
using Xamarin.Forms;
```

```
namespace SimpleTextApp
{
class MainPage: ContentPage
{
public MainPage ()
{
}
}
}
```

Note that I got rid of all unnecessary name ranges (however any unused name range will appear in the code in a faint color in the Visual Studio 2015 development environment). The MainPage class will play the role of a simple content page for the SimpleTextApp application. We will include in this category the code needed to create a single Label containing simple text. Then we will do some simple experiments on this label. This program is actually simple, and its mission is to make you more familiar with Xamarin.

We will start by creating a label from the Label class within the MainPage class builder. Labels are typically used to display text to the user. Look at the following simple code:

```
Label lblMain = new Label ();
 lblMain.Text = "Welcome to moaml Academy!";
```

We create a label and create any object of a class. We set up a new code in the previous object of the class and Label to the variable lblMain. Then assign text "Welcome to Hsoub Academy!" to the Text property of the variable lblMain. The Text property is used to set and read the text content of a label.

So that we can view the previous label on the home page of the application, we assign variable lblMain to the Content property of the class ContentPage. Since the MainPage class inherits from the ContentPage, the Content property is automatically included within it. The attribution process will be as follows:

```
this.Content = lblMain;
```

Previous attribution process is possible because the class inherits from Label Class View, which represents a general view display interface concept. Since the Content property is also of type View, this attribution is possible. The contents of the MainPage.cs file will be similar to the following:

```
using Xamarin.Forms;

namespace SimpleTextApp
{
    class MainPage: ContentPage
    {
    public MainPage ()
        {
    Label lblMain = new Label ();
    lblMain.Text = "Welcome to moaml Academy!";

    this.Content = lblMain;
        }
    }
}
```

That's it! Now we have to do a small step last, which is to make our application creates a new object of our class as part of the MainPage file App.cs. Navigate to this file (located within the project (SimpleTextApp (Portable and make sure to be the builder of Class App on the following figure:

```
public App ()
{
// The root page of your application
MainPage = new MainPage ();
}
```

Now press the F5 key to execute the application, to get a shape similar to the following:

**Welcome to moaml Academy!**

## 小

大家好！

插入的内容要能正常显示才是比较好的。

这是第二行内容。

Note that I dropped the lblMain variable because we assigned the Label object directly to the Content property.

### Additional advantages over the app:

You will notice from the previous application that the sticker appears in the upper left corner of the window. We'll make it appear in the center of the screen. Two adjective properties should be set for this purpose:
HorizontalOptions (for horizontal alignment options) and VerticalOptions (for vertical alignment options). Both of these properties are of type LayoutOptions, a struct structure that exists within the domain name Xamarin.Forms. This structure contains several ready-made fields that are useful for horizontal and vertical positioning options for the label, which are very important options as we will see later in this series. Let us now make the required modification to the label within the MainPage class builder. The contents of the MainPage.cs file will look like this:

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
