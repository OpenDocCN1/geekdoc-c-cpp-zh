
When you first see Expression Blend, like the screenshot shown in Figure 7.3, it can be a little overwhelming. Those of you who have used tools like Adobe Photoshop will almost immediately recognize all the core elements of a design tool. For developers like me, who tend to throw garlic and holy water at design tools like Photoshop, getting used to this application took a little time.

As I progress throughout this section and in the tutorial in this chapter, I might talk about visual controls and other things with which you aren’t yet familiar. Don’t worry about that and just go with the flow; everything that I do in this chapter with Blend will be explained in greater detail with C# and XAML in later chapters, including the stock controls, panels, building custom controls, and the animation system.

![](img/04a00d46bb1059867d95707babd62ee7_85_0.png)

Figure 7.3 Expression Blend after opening a VS solution.

You can launch Expression Blend directly from your Start menu, or you can launch it already set to your current Visual Studio project by clicking Project, Open in Expression Blend from inside Visual Studio with an open WP7 application. On the left in the first panel you’ll see a tab called Projects. This tree should look very similar to the Visual Studio Solution Explorer. This gives you a file system-based view of your solution. When you double-click an XAML file in this view, it will appear in the design view in the middle.

Below the first panel is an Objects and Timeline view. This gives you a hierarchical view of the objects discovered inside the current XAML file. As you can see in the screenshots in Figures 7.3 and 7.4, the root object is an instance of PhoneApplicationPage, which contains a TitlePanel and a ContentGrid, and inside that ContentGrid is a Pivot control named mainPivot. Items in this view show up as their data types when those elements haven’t been assigned a name.

![](img/04a00d46bb1059867d95707babd62ee7_86_0.png)

Figure 7.4 Editing different Pivot items directly in the designer.

Figure 7.4 shows how you can quickly and easily use the Objects and Timeline view to navigate directly to the item you want to edit. In this case, we are editing a PivotItem within a Pivot control. To do this in a pure-XAML text view, you would have to scroll down through all the XML content looking for the control you wanted to edit. The Objects and Timeline panel can be an incredible timesaver.

On the right side of the screen, as shown in either Figure 7.3 or 7.4, you can see a bunch of editing panels. The first is the Properties window, which allows you to edit the properties of a control. Notice that whenever a property can be set to a type of Brush, the Blend Properties window gives you a nice Brush editing tool. You can quickly use this tool to set backgrounds to be transparent, solid colors, or even gradients. Again, setting Brush properties using Blend is much easier than doing it by hand.

There are hundreds of different things you can do with the Properties window and with the selection tool. In Figure 7.4 you can see that there are little padlock icons on various key points in the selection highlight around my control. I can easily use those little padlocks to set how my control automatically resizes itself within a parent control, or I can set the height and width to fixed numbers. The possibilities are not infinite, but a developer or designer familiar with Expression Blend and its capabilities, and who has a bit of creativity, can truly create amazing user experiences.

Another feature I really like about Expression Blend is the capability to use annotations. Annotations give teams the capability to leave comments about particular UI elements so that other team members can see them and respond to them accordingly. For example, in Figure 7.5 I’ve left my team members a little sticky note directly in the Blend UI complaining about some UI elements that I don’t like.

![](img/04a00d46bb1059867d95707babd62ee7_87_0.png)

Figure 7.5 Using annotations to take notes and share with the team.

The presence of this annotation modifies the underlying XAML to include the following new XAML namespace:

```
xmlns:Anno="http://schemas.microsoft.com/expression/blend/extensions/annotations/2008"
```

In addition, the annotation is added to whatever target control I was referencing at the time by adding an element as a dependency property, as shown in the following XAML that corresponds to the sticky note in Figure 7.5:

```
<Anno:AnnotationManager.Annotations>
    <Anno:Annotation AuthorInitials="K" Author="Kevin" Left="496" SerialNumber="1" Top="137" Timestamp="12/20/2010 00:12:01" Text="I think this box needs to be changed a little. There should be explosions, and animated dripping blood, bouncing corpses, and brain-eating zombies all over this UI!!"/>
</Anno:AnnotationManager.Annotations>
```

If another person on my team checked out the code (which includes the annotated XAML) from our source control repository, he would then be able to see my feedback and respond to it (hopefully without using foul language). One caveat here is that I have found that the presence of these annotations in a WP7 project can cause the built-in Visual Studio design surface to occasionally hiccup and be unable to render the UI. This has no effect on whether the application will run properly, but it can be annoying. I suggest not using annotations unless you and your team are planning to use Blend for your primary design surface, and the design surface is either off or minimally used within Visual Studio.

## Blend Tutorial—Working with Visual States

In this section of the chapter I’m going to walk you through a simple Blend tutorial by starting fresh with a new WP7 application. This should give you some familiarity with the application and hopefully teach you a little something about an often underrated feature of Silverlight controls: the Visual State manager.

Visual states are, as the name implies, different states in which a control can be. These states are visual because the end user can visually tell the difference between those states. Stock controls come with their own built-in set of states, but you can also create your own states at the control- or even page-level.

For example, the standard Button control has several states already defined, including: Normal, MouseOver, Pressed, and Disabled. Don’t worry about MouseOver, that’s a holdover from the fact that WP7 is actually Silverlight under the hood, and the desktop version of Silverlight supports mouse movement. There is no finger gesture on a Windows Phone 7 device that can simulate the mouse-over movement because the device doesn’t know where your finger is until you actually tap the screen.

The truly awesome thing about these visual states is that not only can you supply your own styles for each of these states, but you can also control the transition between these states. If you wanted to, you could make a button rotate between the Normal and Disabled states, making the button flip over and bounce a little and do a little “death” animation when it transitions into the Disabled state. Although there might not be much cause for this kind of thing, knowing that you can do it without writing your own custom Button control can come in quite handy.

In this tutorial, we’re going to make a button that has a different style for the Pressed state. In a stock WP7 application, the button style is either white-on-black or black-on-white. When you press (tap) down on the button, it inverts this style. For example, if your UI is configured in “dark” mode, the normal button state is white-on-black and when you tap down on it, it flips to black-on-white. I want to make it so that tapping on my button switches to a green background color.

To get started, create a new WP7 project in Visual Studio. In Visual Studio, click the File menu item; then click New, Project. From here, click the Silverlight for Windows Phone category on the left and make sure Windows Phone Application is selected on the right. Type in a name for the project, and then click OK.
