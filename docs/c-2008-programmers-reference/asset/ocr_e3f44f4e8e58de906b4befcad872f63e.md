Now double-click on the Page.xaml.js file in the Project window to open it. Declare the following global variables at the top of the file:

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

When the page is loaded, get a reference to all the major controls on the page:

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

# Creating the Helper Functions

Two helper functions — ConvertToTimeSpan() and DisplayCurrentPlayBack() — need to be defined.