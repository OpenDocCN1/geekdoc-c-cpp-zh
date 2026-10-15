
Take some time now to go back through the project you’ve been working on in Blend throughout this tutorial. Explore, click, and break things. Play around with all the panes, panels, and properties that you can find. I highly recommend poking around with things so much that you feel completely and utterly lost and overwhelmed. It’s at that point where you can take a step back and go on with the rest of the chapters in this book. As you go through the subsequent chapters, all those foggy areas in your head and the questions you had about Blend, XAML, C#, and WP7 will eventually be answered, and lights will go on in your head. I’ve found that when learning new technology, having that initial experience of diving in and feeling completely lost helps guide my learning in the future. It makes the “light bulb” moments in the future that much more memorable, and I retain that information longer.

## Summary

This chapter provided you with an overview of Apple’s design tool for Xcode, Interface Builder. I then compared Interface Builder with Microsoft’s design tool, Expression Blend. We went through the basics of how to operate Blend, how to use Blend to create a Windows Phone 7 application, and finally we walked through a tutorial of how to use visual states and the Visual State Manager from Blend and Visual Studio.

At this point you should have a good idea of what it will look and feel like to build WP7 applications using Expression Blend and Visual Studio. You probably have a lot of questions, and a lot of the controls used in this chapter might not make much sense. This is a good thing. Your curiosity will help keep you going throughout the rest of the book and will make the new information sink in deeper as you learn more about WP7 programming.

This page intentionally left blank

## Using Basic UI Elements

> The public is more familiar with bad design than good design.
> It is, in effect, conditioned to prefer bad design, because that is what it lives with.
> The new becomes threatening, the old reassuring.
> 
> Paul Rand

This chapter provides an overview of the basic UI building blocks that are available to Windows Phone 7 developers and relates them to the building blocks that iOS developers might already be familiar with. iOS developers should pay special attention to the section on layout and panels because things like flow panels and automatically adjusting grids simply do not exist in iOS and can save you a lot of hard work when used well.

When you have reached the end of this chapter, you should have a good idea of the basic arsenal of UI weaponry available to you to thwart your enemy (the empty design surface). You will learn about displaying and prompting for text, displaying buttons and reacting to button presses, layout panels, images, and even basic animation. This should provide you with a solid foundation on which to continue throughout the rest of the book as you make more compelling and complex applications.

## Using the Basic Controls

This next section will take you on a tour through the basic building blocks of a Silverlight UI on Windows Phone 7. These primitive controls are all usable and quite powerful in their basic form but, as you will see in later chapters, the use of templates, inheritance, and other customizations can turn these building blocks into incredible controls that produce amazing user interfaces.

Try not to assume that because these controls are “primitive” that you should skip right past this section. iOS developers know the intrinsic value of primitive controls and how inheriting from them and customizing them can make the difference between a bland UI and an eye-popping UI that earns an app top billing in the App Store.

## Using Text Blocks

One of the most common activities you will be doing when building your user interface is displaying text. Whether this text is data-bound and came from a web service, or whether it is static text displaying a greeting, the basic building block for rendering text is the TextBlock control.

Although I am aware that you can use Expression Blend to manipulate your UI and drag all these controls visually onto your design surface, I firmly believe in knowing the plumbing that makes everything work. As such, unless Expression Blend is specifically required or substantially simplifies a task, I will be showing you the XAML to build the control rather than screenshots of how to configure it in Expression Blend.

To get started, you can follow along by creating your own Windows Phone 7 project in Visual Studio 2010 and call it BasicControls. To create a Windows Phone 7 project, choose the Windows Phone Application project template from the Silverlight for Windows Phone template category.

### Note

> Whenever I refer to Visual Studio 2010 or simply Visual Studio, I am referring to either of the following: the full development version of Visual Studio 2010 that many developers might already have on their computers prior to downloading the WP7 SDK, or the WP7-specific "lite" version of Visual Studio 2010 that you receive when you install the WP7 SDK on a computer that had no previous installation of Visual Studio 2010. Throughout this book you can assume that any reference to Visual Studio can be applied equally to either product unless a difference is otherwise noted. For example, when it comes time to build service-oriented back-ends to support your WP7 application, you might need to install the full version of Visual Studio 2010 for some features.

After you have created your empty application, you'll see that inside the MainPage.xaml file are a couple of TextBlocks already created for you. I've just changed the text of these, as shown in Listing 8.1.

### Listing 8.1 Text Blocks in XAML

```
<TextBlock x:Name="ApplicationTitle"
    Text="SAMPLE APPLICATION"
    Style="{StaticResource PhoneTextNormalStyle}"/>
<TextBlock x:Name="PageTitle"
    Text="This is a test"
    Margin="9,-7,0,0"
    Style="{StaticResource PhoneTextTitle1Style}"/>
```

One thing that makes working with these controls declaratively so easy is that you can add an event handler to the control just by typing a few letters. Press Enter after the line of code that configures the Margin attribute for the PageTitle TextBlock. As soon as you start typing (type the letter M), you will see a drop-down box appear with a list of possible completions for whatever you're typing. The event you're looking for is MouseLeftButtonUp. Type the equal sign (=) after the word MouseLeftButtonUp and then press Tab. This automatically creates a piece of code in the code-behind for your XAML page that responds to the MouseLeftButtonUp (essentially the end of a single tap) event.

Press F7 to see the code-behind. Modify your code so that the MainPage class looks like the one defined in Listing 8.2.

### Listing 8.2 Responding to a Single Tap on a TextBlock

```
namespace BasicControls
{
    public partial class MainPage : PhoneApplicationPage
    {
        // Constructor
        public MainPage()
        {
            InitializeComponent();
        }

        private void PageTitle_MouseLeftButtonUp(
            object sender, MouseButtonEventArgs e)
        {
            MessageBox.Show("You tapped the page title, " +
                (sender as TextBlock).Text);
        }
    }
}
```

The preceding code shows you how to create a simple event handler to allow your application to execute some code whenever the user taps on the page title. Just about every control is tappable, including controls that you might not think about, such as TextBlocks. We use the as keyword in C# to typecast the sender object to a TextBlock object so that we can access its Text property.

The MessageBox class is a static class that provides a few methods for displaying a modal box on top of other user interface elements. For iOS developers, a control with a nearly identical purpose is the UIAlertView control that you might invoke using the following code:

```
UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Alert" message:@"You tapped the page title."
```
