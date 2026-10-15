
```
delegate:self
cancelButtonTitle:@"Cancel"
otherButtonTitles:nil] autorelease];
[alert show];
```

Then you might provide your own delegate code that responds to various button presses on your alert view. As you can see, for standard alert messages, the MessageBox class is easier and simpler to use.

Figure 8.1 illustrates what happens when you tap the title of this application.

![](img/04a00d46bb1059867d95707babd62ee7_98_0.png)

Figure 8.1 A message box displayed in response to tapping a TextBlock.

As you progress through the book, you will see a variety of things you can do with the seemingly basic and primitive TextBlock control. Remember that you can style virtually all aspects of any control, including the rendering color, and even create custom special effects that attach to any visual element.

## Accepting User Input with TextBoxes

Most applications are not read-only displays. At some point you will probably have to break down and actually ask your users for some input, whether you like it or not. To do that, you’re going to need a TextBox. As its name says, a TextBox is a box in which a user can supply text.

The user does this in one of two ways. The first, which is available on all Windows Phone 7 devices, is through the use of the onscreen soft keyboard. When a user taps inside the region of a TextBox, the keyboard will appear, allowing the user to enter text by tapping on the virtual keys. The second method is through an actual hard keyboard that is available only if the user has purchased a phone with a physical keyboard. At the time of the Windows Phone 7 launch, several manufacturers had slide-out keyboards, and one even had slide-out speakers (but only a touchscreen keyboard).

Whether a user is typing on a real keyboard or a virtual touch-screen keyboard, the TextBox control accepts the input the same and isolates the developer from having to write custom code to handle both situations.

Add the XAML code from Listing 8.3 below the last TextBlock from Listing 8.1 to create a new label and a text box for entering text.

### Listing 8.3 Adding a Label and TextBox

```
<TextBlock x:Name="ApplicationTitle"
    Text="SAMPLE APPLICATION"
    Style="{StaticResource PhoneTextNormalStyle}"/>
<TextBlock x:Name="PageTitle"
    Text="This is a test"
    Margin="9,-7,0,0"
    MouseLeftButtonUp="PageTitle_MouseLeftButtonUp"
    Style="{StaticResource PhoneTextTitle1Style}"/>

<TextBlock x:Name="SampleLabel"
    Text="Enter some text:" />
<TextBox x:Name="SampleTextBox" />
```

Now change the code for the “single tap” event handler on the page title to the code shown in Listing 8.4 and the modal dialog box that appears will contain the text the user supplied in the text box rather than the fixed title of the page.

### Listing 8.4 Reading Text Property of a TextBox

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

        private void PageTitle_MouseLeftButtonUp(object sender,
            MouseButtonEventArgs e)
        {
            MessageBox.Show("You tapped the page title, " +
SampleTextBox.Text );
    }
}
}
```

In the preceding code listing, we are accessing the Text property on the SampleTextBox control that contains the text input into that control by the user, if any more. You can do a lot more with a text box, but this should whet your appetite for user input on the Windows Phone.

Run the sample project again and type something into the text box before you tap the page title. When you tap the page title you should see whatever text you entered in the box appear in the modal pop-up.

## Working with Buttons

Buttons are an essential part of any user interface. They provide nice, easy-to-hit targets for your fingers. We use buttons to cause actions to occur. In general, you can think of a button as the user interface equivalent of a verb. When something needs to be done, you tap a button to get it done. Of course, this is just an example, and there are many examples of user interfaces where buttons are used more creatively or even not used at all.

If you don’t already have it open, launch Visual Studio and bring up the project that we’ve been working on throughout this chapter. Open up the MainPage.xaml file and scroll down to the last control you added in Listing 8.3. Add the buttons shown in Listing 8.5.

### Listing 8.5 Adding Buttons to the Page

```
<Button x:Name="TestButtonOne">
    <TextBlock Text="Zombies are your friends" />
</Button>
<Button x:Name="TestButtonTwo" Click="TestButtonTwo_Click">
    <Border BorderBrush="Yellow" BorderThickness="3" CornerRadius="15">
        <TextBlock Margin="5,5,5,5" Text="Some Text"></TextBlock>
    </Border>
</Button>
```

The first button is self-explanatory. It has a name and it has child content in the form of a TextBlock. This is your first example of a templated control, and you will see hundreds of these as you progress through this book. The child content of the button, no matter what it is, is wrapped up inside the functionality that makes a button a button—the capability to respond to a mouse click (or, in the case of WP7, a finger tap).

The next button (named TestButtonTwo) is a little more interesting. The first child element of this button is a Border control. A Border control does just what its name implies—it wraps whatever child content it contains with a configurable border. In our case, we wrapped the child content in a yellow border that is 3 points thick with a

```
MessageBox.Show("You tapped the page title, " +
    SampleTextBox.Text);
}

private void TestButtonTwo_Click(object sender,
    RoutedEventArgs e)
{
    MessageBox.Show(
        "You tapped the button with nested controls!");
}
}
```

One thing worth pointing out is that the UIButton control in iOS has very similar functionality. Whereas the default behavior of a WP7 button is to appear as a square with a border around the child controls, the UIButton is more purpose-driven. It contains a property called buttonType that controls the button’s core behavior and can be any of the following values: UIButtonTypeCustom, UIButtonTypeRoundedRect, UIButtonTypeDetailDisclosure, UIButtonTypeInfoLight, UIButtonTypeInfoDark, or UIButtonTypeContactAdd. The purposes of these different button types should be fairly self-explanatory to any iOS developer or even any well-versed iPhone user.

## Philosophical Differences in SDK Design

The default implementation of buttons in WP7 and iOS is a classic example of how the SDK design philosophy differs between WP7 and iOS, and on a larger scale, the .NET Framework and Cocoa. The UI controls that come with the iOS SDK are all purpose-driven. They make accomplishing a certain task with a very iPhone-ish look and feel very easy. The main goal of the iOS SDK is to remove as many obstacles as possible between you and building an application that looks and behaves exactly like most of the stock applications. So, if you want a button with rounded edges or an info button with a light icon (both of which occur in copious quantities throughout the core OS), you have very little work to do. However, if you want to create a custom button in iOS with custom visuals inside the bounding frame, you have a lot of work to do.

Conversely, the goal of the .NET Framework and specifically Silverlight for Windows Phone 7 is to make any and all possible user interfaces equally available to you. It is a debate of breadth versus depth. iOS hides the complexity of customization behind a façade of extremely purpose-driven controls that will get you to the 80% point (in general) faster than you might in Silverlight. However, the last 20%, where customization and tweaking typically occurs, can be a frustrating, nail-biting, hair-removing experience in iOS, whereas the entire 100% of the development process in Silverlight typically requires the same level of effort.

Neither SDK design is the only right or wrong design, but both were clearly built for different audiences and different purposes. Silverlight makes doing amazing things with your UI just as easy as doing the mundane, whereas iOS makes the mundane nearly automatic and offloads that saved effort into the realm of customization.
