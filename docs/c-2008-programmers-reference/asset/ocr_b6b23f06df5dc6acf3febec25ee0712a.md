# Part II: Application Development Using C#

(continued)

```
// Retrieve the div element you created in the previous step.
var parentElement = 
    document.getElementById("SilverlightPluginHost");

    // creates the Silverlight plug-in.
    createSilverlightPlugin();
</script>

</body>
</html>
```

This HTML file is the page that will host the Silverlight plug-in. Notice that it references two JavaScript files:

+   - [ ] Silverlight.js
+   - [ ] MySilverlight.js

You’ve already added the first one. Now, using Notepad, create the following JavaScript file; name it MySilverlight.js, and save it in C:\Silverlight\.

```
function createSilverlightPlugin()
{
    Silverlight.createObject(
        "UI.xaml",          // Source property value
        parentElement,      // DOM reference to hosting DIV tag.
        "mySilverlightPlugin", // Unique plug-in ID value.
        {                   // Per-instance properties.
            width:'300',    // Width of rectangular region of
                            // plug-in area in pixels.
            height:'300',   // Height of rectangular region of
                            // plug-in area in pixels.
            inplaceInstallPrompt:false, // Determines whether to display
                                        // in-place install prompt if
                                        // invalid version detected.
            background:'#D6D6D6', // Background color of plug-in.
            isWindowless:'false', // Determines whether to display
                                  // plug-in in Windowless mode.
            framerate:'24',     // MaxFrameRate property value.
            version:'1.0'       // Silverlight version to use.
        },
        {
            onError:null,       // OnError property value --
                                // event handler function name.
            onLoad:null         // OnLoad property value --
                                // event handler function name.
        },
        null);              // Context value -- event handler
                            // function name.
}
```

This JavaScript file contains the logic behind your Silverlight application. It loads the Silverlight plug-in as well as the XAML file (UI.xaml, which is defined in the next section).