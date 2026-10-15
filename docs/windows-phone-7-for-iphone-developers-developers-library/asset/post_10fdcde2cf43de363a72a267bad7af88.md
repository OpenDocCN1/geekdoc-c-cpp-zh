
# Using Advanced UI Elements

> *Form follows function—that has been misunderstood.
> Form and function should be one, joined in a spiritual union.*
> 
> Frank Lloyd Wright

This chapter focuses specifically on translating your knowledge of certain types of applications and application components from iOS to Windows Phone 7. Even if you aren’t an iOS developer, you might learn a few things about how these various application components look on the iPhone.

When building iOS applications, you’ll see a few types of application components reused over and over, to the point where these components are immediately recognizable in virtually any iOS app, no matter how much they have been customized.

The navigation bar is used in so many applications it is almost hard to find one that doesn’t use it. Next, this chapter covers the use of tab bar applications and how you might migrate a tab bar application to have the same functionality but make use of native WP7 UI elements. Finally, this chapter covers what is arguably the single most used controller in the iOS SDK: the Table View Controller. This last section of the chapter covers the variety of options available to developers wanting to migrate Table View Controller apps to Windows Phone 7.

## Migrating from Navigation Bars

Building iOS applications with navigation controllers is almost second nature to virtually any iOS developer. Not only does Xcode come with a built-in template for building a navigation application, but Interface Builder (or just Xcode in v4+) makes it incredibly easy to add a navigation controller to any interface.

The purpose of the navigation controller is to make navigating hierarchies of screens easy. The controller comes with built-in facilities for supplying each view with a title, back buttons, and even control “knobs” like edit buttons that can inform other parts of the UI to switch from a read-only mode to a view mode.

As I have said multiple times so far in this book, the iOS SDK is purpose-driven. The navigation controller is a clear example of that. Apple wanted to make the experience of navigating through screens smooth and, more importantly, consistent. Anyone who has used an iPhone is aware of this consistency because the ubiquitous nature of the navigation controller coupled with its consistent look and feel make the act of going back (or “up” a hierarchy), drilling down, or changing screen state almost instinctive.

There is no direct correlation for a navigation controller in the Windows Phone 7 SDK, but a couple of controls and a complete navigation subsystem make rolling your own navigable UI quite easy. First we’ll take a look at the Silverlight navigation system (available both in regular and WP7 versions of Silverlight), and then we’ll take a look at some possible ways we can put a nice easy UI on top of this system, and even consider a few scenarios when we wouldn’t want a navigation UI.

Figure 9.1 is a screenshot of the FB Investor iPhone App that follows the activity of the folks on the FortuneBuilders team. At the top of this screenshot you can see a navigation controller. These controllers typically have a view that manifests itself as this top bar. The middle of the bar is reserved for the title of the current view in the hierarchy, and the left side stays empty until there is a view that you can navigate back to, as shown in Figure 9.2.

![](img/04a00d46bb1059867d95707babd62ee7_118_0.png)

Figure 9.1   An iOS navigation controller at the top of a hierarchy.

![](img/04a00d46bb1059867d95707babd62ee7_119_0.png)

Figure 9.2 An iOS navigation controller in the middle of a hierarchy.

Figure 9.2 shows an iOS navigation controller that is at least one level deep in a view tree or hierarchy. You can see by the title of the back button that tapping it will take you back to a view titled Posts, and the current view is one that displays the contents of a blog post.

The next few sections will show you how to produce this kind of functionality (although not quite the same UI) on Windows Phone 7 using Silverlight.

## Using the Silverlight Navigation System

The Silverlight navigation system is an API exposed through a single object, the NavigationService object that is a property of the Page object. It maintains a basic navigation trail as the user moves through an application.

The CanGoForward and CanGoBackward properties provide developers with a basic way of interrogating the user's navigation history. If either of these properties are true, the GoForward() and GoBack() methods can be invoked, respectively. If you attempt to invoke either of these methods when navigation in that direction is not possible, an exception will be thrown. To be safe and to avoid throwing unnecessary exceptions, always check the values of these properties before performing the actual navigation. To move the user from one page to another, use the Navigate() method.

Although this might seem like a simple concept, it helps to see it in action to see how everything works. To do this, create a new Windows Phone application, which will create a portrait-based main page. On the MainPage.xaml, add a new button called

navigateButton. The following code snippet shows the Click event handler for this button:

```
private void navigateButton_Click(object sender, RoutedEventArgs e)
{
    NavigationService.Navigate(new Uri("/Page1.xaml", UriKind.Relative));
}
```

This code navigates the user from MainPage.xaml to Page1.xaml instantly. The fact that the user originated on MainPage.xaml will be stored in the navigation system. When the user lands on the Page1.xaml page, the CanGoBack Boolean property of NavigationSystem will be true. In addition, when the NavigationSystem object's GoBack() method is invoked from Page1.xaml, the user will be sent back to MainPage.xaml.

You can see this in action by adding a new portrait page to the project (leave the default name of Page1). On that page, add a button and set its Click handler to the following:

```
private void backButton_Click(object sender, RoutedEventArgs e)
{
    if (NavigationService.CanGoBack)
        NavigationService.GoBack();
}
```

Note how we checked to see whether backward navigation was possible before calling the GoBack() method. You can also use the Boolean properties CanGoBack and CanGoForward to activate or deactivate various pieces of your own navigation bar control.

### No Forward Movement for WP7

> No matter when you try or how you try, you will never be able to move forward through a navigation hierarchy on Windows Phone 7. Although WP7's version of Silverlight might be nearly identical to that of the desktop version, some differences still exist, and this is one of them. The desktop version of Silverlight allows users to go forward and back, whereas on WP7, the CanGoForward property will never be true and the GoForward() method will always throw an exception.

The actual navigation is just a small part of the system. The real work comes in the pages themselves and how they respond to construction, navigation, and activation. In an iOS application, the developer typically has explicit control over the instantiation of the view controller to which the user will navigate next. This means that the developer also has explicit control over the lifespan of that object.

Using the Silverlight navigation system, the lifespan and activation cycle of these pages might not be immediately obvious. You need to know when and where you can place code that will be executed when pages are first created, when they are loaded, and when a user navigates to the pages. Failure to pay attention to these could cause anything from performance problems to memory issues or worse—your application crashing.

## Using the Page Constructor

Every page object is still just a C# object and, as such, has a regular constructor. When you create a new page object for a WP7 application, it comes with a constructor that invokes the InitializeComponent() method. It looks like the code in the following snippet:

```
public partial class Page1 : PhoneApplicationPage
{
    public Page1()
    {
        InitializeComponent();
    }
}
```

The InitializeComponent() method invokes all the generated code produced by the XAML markup that configures everything according to the markup you see on the design surface. Without delving into too much detail about what goes on inside that method, the key thing to remember is that no objects defined in your user interface will be available for you to use until after this method has been invoked. In short, do not ever create any initialization code in your constructor before the InitializeComponent() method has been called.

The tricky part about page constructors is that they are called only at very specific times. The constructor of the default (first) landing page of an application is called when the application starts up. The constructor of other pages are not called unless you manually instantiate the page or the user navigates to the page through a call to Navigate() on the NavigationService object.

It is possible that at some point during the course of the application’s running, the page will be removed from memory. I will get into the topics of tombstoning and multitasking in later chapters, but for now, keep in mind that it is possible that a page will not remain in memory forever after its constructor has been called, and that its constructor may be called multiple times if the application is “awoken” from a previous suspension.

The reason I bring this up is because people often get into lazy habits of assuming that constructors are absolute, so they use them to fetch whatever data they need and then they assume that data will be around forever.

## Using the Page Loaded Event

One of the problems with relying on the constructor for your initialization code is that the constructor is called very infrequently and often in unpredictable times. The Page’s Loaded event is called, appropriately enough, whenever the page is loaded.

The Loaded event is a low-level event that you will find on most of the UI elements within Silverlight including shapes, buttons, borders, text blocks, and more. You should think of the fact that the page’s Loaded event is called during a navigation as a side effect. Even though you might see a 1:1 correlation between loading and navigation, do not treat them the same. There are more ways than just navigation to load a page, and so there
