
Finally, press F5 to test the application. Click the button and observe the effect (see Figure 19-34).

![](img/a977a875c7c627b45d939729705a252e_668_0.png)

Figure 19-34

## Silverlight 1.0

Animation is one of the core capabilities of Silverlight. The following sections describe how to perform simple animations in Silverlight 1.0.

## Animation — Part 1

You can use the `timeline` object to perform some simple animation. Figure 19-35 shows the page displaying an image. When the mouse hovers over the image, the image will expand. When you move the mouse away, the image returns to its original size.

![](img/a977a875c7c627b45d939729705a252e_668_1.png)

Figure 19-35

## Part II: Application Development Using C#

Using Expression Blend 2, create a new Silverlight project and name it Animations. Add an Image element to the page (see Figure 19-36).

![](img/a977a875c7c627b45d939729705a252e_669_0.png)

Figure 19-36

The XAML source of the page looks like this:

```
<Canvas
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Width="640" Height="480"
    Background="White"
    x:Name="Page">

    <Image Width="165" Height="220" Canvas.Top="70" Canvas.Left="71"/>

</Canvas>
```

Set the Source property of the Image control to reference an image (see Figure 19-37).

![](img/a977a875c7c627b45d939729705a252e_669_1.png)

Figure 19-37

In the Objects and Timeline window, click the + button (see Figure 19-38), use the default name of StoryBoard1, and click OK.

![](img/a977a875c7c627b45d939729705a252e_670_0.png)

Figure 19-38

Click the Record Keyframe button (see Figure 19-39).

![](img/a977a875c7c627b45d939729705a252e_670_1.png)

Figure 19-39

## Part II: Application Development Using C#

Move the yellow timeline (see Figure 19-40) to the 0:00.200 position and click the Record Keyframe button again.

If you like, you can magnify the timeline by setting the Timeline zoom to 500%.

![](img/a977a875c7c627b45d939729705a252e_671_0.png)

Figure 19-40

With the Image element selected, select the Properties Inspector and expand the Transform section. Click on the Scale tab. Set both X and Y to 1.5 (see Figure 19-41).

![](img/a977a875c7c627b45d939729705a252e_671_1.png)

Figure 19-41

Add a second timeline to the project, and use its default name of `StoryBoard2`.

Click the Record Keyframe button, and then in the Properties Inspector's Transform section, click on the Scale tab again. Set both X and Y to 1.5.

Move the yellow timeline to the 0:00.200 position and click the Record Keyframe button again.

In the Properties Inspector's Transform section, click the Scale tab. This time set both X and Y to 1.

Switch the project to XAML view, and add the following highlighted code:

```
<Image Width="165" Height="220" RenderTransformOrigin="1,1" Source="turbinetechnology_1.jpg" x:Name="image" MouseEnter="MouseEnter" MouseLeave="MouseLeave" >
    <Image.RenderTransform>
        <TransformGroup>
            <ScaleTransform ScaleX="1" ScaleY="1"/>
            <SkewTransform AngleX="0" AngleY="0"/>
            <RotateTransform Angle="0"/>
            <TranslateTransform X="0" Y="0"/>
        </TransformGroup>
    </Image.RenderTransform>
</Image>
```

Append the following block of code to Page.xaml.js:

```
function MouseEnter (sender, eventArgs)
{
    var obj = sender.findName("Storyboard1");
    obj.Duration="00:00:00.2000000";
    obj.begin();
}

function MouseLeave (sender, eventArgs)
{
    var obj = sender.findName("Storyboard2");
    obj.Duration="00:00:00.2000000";
    obj.begin();
}
```

Press F5 to test the application. When the mouse now hovers over the image, the MouseEnter event is fired, and the Storyboard1 timeline object is executed for a duration of 0.2 second. The Storyboard1 timeline object basically scales the image horizontally and vertically by 1.5 times. When the mouse leaves the image, the MouseLeave event is fired, and the Storyboard2 timeline object is executed. It scales the image from 1.5 times down to its original size (within 0.2 second; see Figure 19-42).

## Part II: Application Development Using C#

![](img/a977a875c7c627b45d939729705a252e_673_0.png)

Figure 19-42

## Animations — Part 2

Of course, you can perform more complex animation. This section shows you how to make the animation real-life using a KeySpline.

Using Expression Blend 2, create a new Silverlight project and name it animations2.

Add an Image element to the page, and set it to display an image (see Figure 19-43).

![](img/a977a875c7c627b45d939729705a252e_673_1.png)

Figure 19-43

## Chapter 19: Developing Silverlight Applications

Add a Timeline object to the project and use its default name of Storyboard1.

Add two keyframes to time 0:00.000 and 0:01.000, respectively.

At time 0:01.000, click the Translate tab in the Transform section of the Properties Inspector. Set X to 0 and set Y to 250 (see Figure 19-44).

![](img/a977a875c7c627b45d939729705a252e_674_0.png)

Figure 19-44

This will move the image vertically from the top to the bottom.

In the Rotate tab, set the Angle to 360 (see Figure 19-45).

![](img/a977a875c7c627b45d939729705a252e_674_1.png)

Figure 19-45

## Part II: Application Development Using C#

This will cause the image to rotate 360 degrees clockwise.

In the XAML view, add the Loaded attribute to the <Canvas> element:

```
<Canvas Loaded="onLoad">
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Width="640" Height="480"
    Background="White"
    x:Name="Page">

```

Append the following block of code to Page.xaml.js:

```
function onLoad(sender, eventArgs)
{
    var obj = sender.findName("Storyboard1");
    obj.begin();
}
```

Press F5 to test the application. Notice that when the page is loaded, the image drops to the bottom of the page, while rotating clockwise (see Figure 19-46).

![](img/a977a875c7c627b45d939729705a252e_675_0.png)

Figure 19-46

## Slowing the Rate of Fall

To slow down the rate of fall, you can increase the duration of the timeline object. In Storyboard1, move the second keyframe from time 0:01.000 to 0:02.500 (see Figure 19-47).

![](img/a977a875c7c627b45d939729705a252e_676_0.png)

Press F5 to test again. Notice that this time the image fall is longer compared to the previous instance.

## Varying the Rate of Fall

In the previous section, the image drops at a uniform speed. That isn't very realistic, because in real life an object accelerates as it falls. You need to tweak the properties a little to make it more lifelike.

Select the second keyframe (at time 0:02.500) and select the Properties Inspector.

In the Easing section, modify the KeySpline by dragging the yellow dot from the top to the bottom (see Figure 19-48).

![](img/a977a875c7c627b45d939729705a252e_676_1.png)

## Part II: Application Development Using C#

A KeySpline is used to define the progress of an animation. The x-axis of the KeySpline represents time and the y-axis represents value. The KeySpline should now look like Figure 19-49.

![](img/a977a875c7c627b45d939729705a252e_677_0.png)

Figure 19-49

The modified KeySpline means “as time progresses, increase the rate of change.” In this example, it means that as the falling image approaches the bottom, it will drop faster.

Press F5 to test again, and you’ll see that the image accelerates as it nears the bottom. The animation is now more realistic, simulating free-fall.

## Playing Media

One of Silverlight’s key capabilities is a rich media experience. This section examines how to embed a Windows media file in your Silverlight application and how to control its playback. In addition, it also explains how to create simple effects on the video.

## Creating the Silverlight Project

Using Expression Blend 2, create a Silverlight project and name it Media.

## Chapter 19: Developing Silverlight Applications

In the Project window, right-click on the project name (Media) and select Add Existing Item. Select a Windows Media file (WindowsMedia.wmv, for this example; it's included in the book's code download). After this, the WindowsMedia.wmv file will be added to the project.

Double-click WindowsMedia.wmv in the Project window to add it to the page (see Figure 19-50).

![](img/a977a875c7c627b45d939729705a252e_678_0.png)

Figure 19-50

You need Windows Media Player 10 or later for this project to work.

The WindowsMedia.wmv file is now contained within a MediaElement control (see also Figure 19-51):

```
<Canvas
xmlns="http://schemas.microsoft.com/client/2007"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Width="640" Height="480"
Background="White"
x:Name="Page">
<MediaElement x:Name="WindowsMedia_wmv"
Width="320" Height="240"
Source="WindowsMedia.wmv"
Stretch="Fill"
Canvas.Top="8" Canvas.Left="8"
AutoPlay="True"/>
</Canvas>
```
