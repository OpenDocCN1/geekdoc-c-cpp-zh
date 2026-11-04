
## Part II: Application Development Using C#

The MediaEnded event handler is fired when the media has finished playing. You have to make the Play button visible again and hide the Pause button. In addition, you have to move the marker to the beginning and reset the media to the beginning. Here's the code:

```
//---movie has finished playing---
function MediaEnded(sender, eventArgs)
{
    var btnPlay = sender.findName("canvasPlay");
    var btnPause = sender.findName("canvasPause");

    playing = false;
    clearInterval(intervalID);     //---clear the progress updating---
    btnPlay.opacity = 1;           //---show the Play button---
    btnPause.opacity = 0;          //---hide the Pause button---

    //---move the marker to the beginning---
    ellMarker["Canvas.Left"] = -2;
    MediaElement1.Position="00:00:00"; //---reset the movie position---
}
```

The PlayPauseButtonUp button is fired when the user clicks on the Play/Pause button and releases the mouse. When the media has started playing, you use the setInterval() JavaScript function to display the media progress every half second:

```
function PlayPauseButtonUp(sender, eventArgs)
{
    var btnPlay = sender.findName("canvasPlay");
    var btnPause = sender.findName("canvasPause");

    //---if currently playing and now going to pause---
    if (playing == true) {
        MediaElement1.pause();       //---pause the movie---
        clearInterval(intervalID);   //---stop updating the marker---
        playing = false;
        btnPlay.opacity = 1;         //---show the Play button---
        btnPause.opacity = 0;        //---hide the Pause button---
    }
    else
    {
        MediaElement1.play();        //---play the movie---
        playing = true;
        btnPlay.opacity = 0;         //---hide the Play button---
        btnPause.opacity = 1;        //---show the Pause button---

        //---update the progress of the movie---
        intervalID = window.setInterval("DisplayCurrentPlayBack()", 500);
    }
}
```

That's it! Press F5 in Expression Blend 2, and you should be able to use the new media player (see Figure 19-62)!

![](img/a977a875c7c627b45d939729705a252e_698_0.png)

Figure 19-62

## Silverlight 2.0

One of the key strengths of Silverlight is its rich interactive capabilities. Apart from performing cool animations and transformations on graphics and videos, one good use of Silverlight is to develop applications that could not easily be achieved using conventional web applications (even when using ASP.NET and AJAX). A good example is capturing signatures. Often, when you sign for an online service (such as applying for a Google AdSense account) you need to sign a contractual agreement. In place of the traditional signature, you are often requested to provide some sort of personal information (such as your birth date or mother's maiden name) to prove that you are who you are. That's because there is no way you could sign (literally) on the web page, unless you print out the form, sign it, and fax it back to the service provider.

With Silverlight, you can develop an application that allows users to sign on the page itself. And with more and more people using Tablet PCs (or having access to a pen tablet such as the Wacom Intuos Pen Tablet), pen input is no longer a dream. This section shows you how to create a Silverlight 2 application that captures the user's signature. In addition, you'll see how the signature can be sent back to a Web Service for archival.

> Remember to download the Microsoft Silverlight Tools Beta 1 for Visual Studio 2008 tool from www.microsoft.com/downloads before you start the project.

## Part II: Application Development Using C#

## Creating the Project Using Visual Studio 2008

Using Visual Studio 2008, create a new Silverlight project using C# and name it `Signature` (see Figure 19-63).

![](img/a977a875c7c627b45d939729705a252e_699_0.png)

Figure 19-63

> If you have installed the Microsoft Silverlight Tools Beta 1 for Visual Studio 2008 tool, you should see Silverlight in the Project Types list in the New Project dialog.

You will be asked how you want to host your application. Select the second option (Generate an HTML test page to host Silverlight within this project), and click OK (see Figure 19-64).

![](img/a977a875c7c627b45d939729705a252e_699_1.png)

Figure 19-64

Populate Page.xaml as follows:

```xml
<UserControl x:Class="Signature.Page"
xmlns="http://schemas.microsoft.com/client/2007"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Width="400" Height="300">

<Canvas>
    <Canvas x:Name="SigPad" Width="404" Height="152"
        Canvas.Left="8" Canvas.Top="9" Background="#FFFA60C" >
        <Rectangle Width="404" Height="152" Fill="#FFFBFDB"
            Stroke="#FF000000" StrokeThickness="3"/>
    </Canvas>
</Canvas>

</UserControl>
```

The page should now look like Figure 19-65.

![](img/a977a875c7c627b45d939729705a252e_700_0.png)

Figure 19-65

## Capturing the Signature

As the user uses the mouse (or stylus if he/she is using a tablet PC) to write on the control, the series of points it makes on the control will be saved. There will be three events of concern to you:

- MouseLeftButtonDown — Fired when the left mouse button is clicked
- MouseMove — Fired when the mouse moves
- MouseLeftButtonUp — Fired when the left mouse button is released

Figure 19-66 shows what happens when you write the character “C”. When the left mouse button is clicked, the MouseLeftButtonDown event is fired, followed by a series of MouseMove events as the mouse moves counterclockwise, and then finally the MouseLeftButtonUp event is fired when the mouse’s left button is released. As the mouse moves, the series of points made by it are joined together.

## Part II: Application Development Using C#

![](img/a977a875c7c627b45d939729705a252e_701_0.png)

Figure 19-66

The points touched by the mouse between the MouseLeftButtonDown and MouseLeftButtonUp events are saved as a series of continuous points (called a line). For example, the character “C” is made up of one line (assuming that you did not release the left mouse button while drawing it), while the character “t” is made up of two lines — one horizontal and one vertical (see Figure 19-67).

![](img/a977a875c7c627b45d939729705a252e_701_1.png)

Figure 19-67

The points making up an individual line are saved in a generic List object. The individual lines in each character are also saved in a generic List object, as Figure 19-68 shows.

![](img/a977a875c7c627b45d939729705a252e_701_2.png)

Figure 19-68

## Coding the Application

In Page.xaml.cs (see Figure 19-69), declare the following member variables:

![](img/a977a875c7c627b45d939729705a252e_701_3.png)

Figure 19-69

## Part II: Application Development Using C#

The MouseLeftButtonUp event is fired when the user releases the left mouse button. You interpret that as the end of the signature signing process. Code the MouseLeftButtonUp event handler of SigPad as follows:

```csharp
//---fired when the user let go of the left mouse button---
void SigPad_MouseLeftButtonUp(
    object sender, MouseButtonEventArgs e)
{
    //---user has let go of the left mouse button---
    MouseDown = false;

    //---add the list of points to the current line---
    _lines.Add(_points);
}
```

The MouseMove event is fired continuously when the user moves the mouse. Here, you draw a line connecting the previous point with the current point. Code the MouseMove event handler of SigPad as follows:

```csharp
//---fired when the left mouse button is moved---
void SigPad_MouseMove(object sender, MouseEventArgs e)
{
    //---if left mouse button is pressed...---
    if (MouseDown)
    {
        //---add the current point---
        var currentPoint = e.GetPosition(SigPad);
        _points.Add(currentPoint);

        //---draws a line connecting the previous
        // point and the current point---
        Line line = new Line()
        {
            X1 = _previouspoint.X,
            Y1 = _previouspoint.Y,
            X2 = currentPoint.X,
            Y2 = currentPoint.Y,
            StrokeThickness = 2,
            Stroke = new SolidColorBrush(Colors.Black)
        };

        //---add the line to the signature pad---
        SigPad.Children.Add(line);

        //---saves the current point for later use---
        _previouspoint = currentPoint;
    }
}
```

Press F5 to test the application. Use your mouse to draw on the web page (see Figure 19-70).
