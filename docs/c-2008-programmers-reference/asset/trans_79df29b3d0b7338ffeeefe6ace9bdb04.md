
现在，在“项目”窗口中双击 Page.xaml.js 文件将其打开。在文件顶部声明以下全局变量：

```
//---global variables---
var playing = false;
var markerClicked = false;
var duration=0;
var intervalID;

//---all the major elements on the page---
var ellMarker;
var MediaElement1;
var textblock;
var rectProgressWell;
var rectDownloadProgress;
//-------------------------------
```

页面加载时，获取对页面上所有主要控件的引用：

```
MediaPlayer.Page.prototype =
{
    handleLoad: function(control, userContext, rootElement)
    {
        this.control = control;

        //---get a reference to all the major controls on the page---
        MediaElement1 = rootElement.findName("MediaElement1");
        ellMarker = rootElement.findName("ellMarker");
        textblock = rootElement.findName("TextBlock");
        rectProgressWell = rootElement.findName("rectProgressWell");
        rectDownloadProgress =
            rootElement.findName("rectDownloadProgress");
        textblock = rootElement.findName("TextBlock");
        //-----------------------------------------------

        // Sample event hookup:
        rootElement.addEventListener("MouseLeftButtonDown",
            Silverlight.createDelegate(this, this.handleMouseDown));
    },

    // Sample event handler
    handleMouseDown: function(sender, eventArgs)
    {
        // The following line of code shows how to find an element by
        // name and call a method on it.
        // this.control.content.findName("Timeline1").Begin();
    }
}
```

## 创建辅助函数

需要定义两个辅助函数——ConvertToTimeSpan() 和 DisplayCurrentPlayBack()。

## 第 II 部分：使用 C# 进行应用程序开发

ConvertToTimeSpan() 函数将秒数转换为 hh:mm:ss 的 TimeSpan 格式。例如，61 秒会转换为 00:01:01。你需要此函数，因为 MediaElement 控件的 Position 属性只接受 TimeSpan 类型的值。ConvertToTimeSpan() 函数的定义如下：

```
//---convert time in seconds to "hh:mm:ss"---
function ConvertToTimeSpan(timeinseconds)
{
    if (timeinseconds<0) {
        return ("00:00:00");
    }
    else
    if (timeinseconds<60) {
        return ("00:00:" + Math.floor(timeinseconds));
    }
    else
    if (timeinseconds<3600) {
        var mins = Math.floor(timeinseconds / 60);
        var seconds = Math.floor(timeinseconds - (mins * 60));
        return ("00:" + mins + ":" + seconds);
    }
    else
    {
        var hrs = Math.floor(timeinseconds / 3600);
        var mins = timeinseconds - (hrs * 3600);
        var seconds = Math.floor(timeinseconds - (hrs * 3600) - (mins * 60));
        return (hrs + ":" + mins + ":" + seconds);
    }
}
```

DisplayCurrentPlayBack() 函数用于显示媒体播放的当前状态。它显示已播放时间与媒体总时间的对比。例如，如果媒体（总时长为两分钟）播放到第 30 秒，DisplayCurrentPlayBack() 函数会显示 00:00:30 / 00:02:00。此外，该函数还负责在媒体播放时同步标记。为确保播放状态持续更新，你会使用 setInterval() JavaScript 函数反复调用 DisplayCurrentPlayBack()（稍后详细介绍）。DisplayCurrentPlayBack() 函数的定义如下：

```
//---shows the current playback -- marker and position---
function DisplayCurrentPlayBack()
{
    //---find duration of movie---
    if (duration==0)
        duration = Math.round(MediaElement1.NaturalDuration.Seconds * 100) /
            100;

    //---find current position---
    var position = MediaElement1.Position.Seconds;

    //---move the marker---
```

```
ellMarker["Canvas.Left"] = Math.round((position / duration) * rectProgressWell.width);

//---format - elapsed time/total time---
var str = ConvertToTimeSpan(position) + " / " + ConvertToTimeSpan(duration);

textblock.Text = str;
}
```

## 定义事件处理程序

最后，定义各种事件处理程序。

当 MediaElement 控件从远程服务器下载媒体时，DownloadProgressChanged 事件处理程序会持续触发。在此事件处理程序中，首先获取进度值（从 0 到 1），然后在 TextBlock 控件上显示下载百分比。此外，还要调整 rectProgressWell 控件的宽度，使媒体下载时其宽度扩大（见图 19-61）。代码如下：

```
//---fired while the movie is being downloaded---
function DownloadProgressChanged(sender, eventArgs)
{
  //---get the progress value from 0 to 1---
  var progress = MediaElement1.DownloadProgress;

  //---display the download in percentage---
  textblock.Text = Math.round(progress*100).toString() + "%";

  //---adjust the width of the progress bar---
  var progressWidth = progress * rectProgressWell.width;
  rectDownloadProgress.width = Math.round(progressWidth);
}
```

![](img/a977a875c7c627b45d939729705a252e_694_0.png)

图 19-61

当用户单击标记（Ellipse 元素）时，会触发 EllMarkerDown 事件处理程序。这里，将 markerClicked 变量设置为 true，以指示标记已被单击：

```
//---marker is clicked---
function EllMarkerMouseDown(sender, eventArgs)
{
  markerClicked = true;
}
```

当用户释放鼠标按钮时，会触发 EllMarkerMouseUp 事件处理程序。首先需要检查用户是在主画布本身还是在标记上释放按钮。如果之前单击过标记，则需要将标记移动到鼠标当前位置，并将媒体设置为新位置。影片的新位置由媒体时长乘以标记位置相对于进度条宽度的比例确定。代码如下：

```
//---marker is released---
function EllMarkerMouseUp(sender, eventArgs)
{
    //---only execute this function if the user is moving the marker---
    if (markerClicked)
    {
        //---find duration of movie---
        duration = Math.round(MediaElement1.NaturalDuration.Seconds * 100)/100;

        //---get the position of the marker w.r.t. to the Well---
        position = ((ellMarker["Canvas.Left"]) / rectProgressWell.width) * duration;

        //---get integer part---
        position = Math.floor(position);

        //---end of the media---
        if ((ellMarker["Canvas.Left"]==rectProgressWell.width)) {
            //---move the movie to the last frame---
            MediaElement1.Position = ConvertToTimeSpan(duration);
        }
        else
        {
            //---move the movie to the new position---
            MediaElement1.Position = ConvertToTimeSpan(position);
        }
    }
}
```

当鼠标在页面上移动时，MediaPlayerMouseMove 事件处理程序会持续触发。需要判断鼠标移动时标记是否被单击。如果是，则表示用户正在移动标记，需要重新定位标记。代码如下：

```
//---mouse moves inside the Silverlight media player control---
function MediaPlayerMouseMove(sender, eventArgs)
{
    //---user clicks marker and drags it---
    if (markerClicked)
    {
        //---find duration of movie---
        if (duration==0)
            duration = Math.round(MediaElement1.NaturalDuration.Seconds * 100)
                / 100;

        clearInterval(intervalID);

        //---get the position of the mouse with respect to the progress Well---
```

```
var pt = eventArgs.getPosition(rectProgressWell);

//---marker not allowed to stray outside the well---
if (pt.x > 0 && pt.x < rectProgressWell.width)
{
    //---moves the marker---
    ellMarker['Canvas.Left'] = pt.x;

    //---display the new time---
    textblock.Text = ConvertToTimeSpan((pt.x / rectProgressWell.width)
        * duration).toString();
}
else
if (pt.x <= 0)  //---move to the beginning---
{
    //---moves the marker---
    ellMarker['Canvas.Left'] = 0;

    //---display the new time---
    textblock.Text = "00:00:00";
}
else
if (pt.x >= rectProgressWell.width) //---move to the end---
{
    //---moves the marker---
    ellMarker['Canvas.Left'] = rectProgressWell.width;

    //---display the new time---
    textblock.Text = ConvertToTimeSpan(duration);
}

if (playing)
    intervalID = window.setInterval("DisplayCurrentPlayBack()", 500);
}
```

当鼠标离开 Silverlight 页面时，会触发 MediaPlayerMouseLeave 事件处理程序。在这种情况下，将 markerClicked 变量设置为 false：

```
//---mouse leaves the entire Silverlight media player control
function MediaPlayerMouseLeave(sender, eventArgs)
{
    markerClicked=false;
}
```
