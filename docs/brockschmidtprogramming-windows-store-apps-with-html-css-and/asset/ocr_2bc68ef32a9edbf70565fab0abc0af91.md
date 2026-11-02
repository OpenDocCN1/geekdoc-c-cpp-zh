For example, one of the early partners I worked with had a method to retrieve a localized URI to their back-end services, which was failing in design mode. Using the design mode flag, then, we just had to change the code to look like this:

```
WinJS.Namespace.define("App.Localization", {
    getBaseUri: function () {
        if (Windows.ApplicationModel.DesignMode.designModeEnabled) {
            return "www.default-base-service.com";
        } else {
            var resources = new Windows.ApplicationModel.Resources.ResourceLoader();
            var baseUri = resources.getString("baseUri");
            return baseUri;
        }
    }
});
```

Alternately, you could create a hidden element in the DOM that uses data-win-res to load the string into itself and then have a function like the below retrieve that string:

```
<!--In markup -->
<div id="baseUri" data-win-res="textContent: 'baseUri'" style="display: none;"></div>
```

```
//In code
WinJS.Namespace.define("App.Localization", {
    getBaseUri: function () {
        return document.getElementById("baseUri").textContent;
    }
});
```

Finally, it is possible to have custom controls show up in the Assets tab alongside the HTML elements and the WinJS controls. For this you'll first need an OpenAjax Metadata XML (OAM) file that provides all the necessary information for the control, and you already have plenty of references to draw from. To find them, search for *.oam.xml files within Program Files (x86). You should find some under the Microsoft Visual Studio 12.0 folder and deep down within Microsoft SDKs where WinJS metadata lives. In both places you'll also find plenty of examples of the 12x12 and 16x16 icons you'll want for your control.

If you look in the controls/calendar folder of the CalendarControl example with this chapter, you'll find calendar_oam.xml and two icons alongside the js and css files. The OAM file, which must have a filename ending in _oam.xml, tells Blend how to display the control in its Assets panel and what code it should insert when you drag and drop the control into an HTML file. Here are the contents of that file:

```
<?xml version="1.0" encoding="utf-8"?>
<!-- Use underscores or periods in the id and name, not spaces. -->
<widget version="2.0"
    spec="2.0"
    id="http://www.kraigbrockschmidt.com/schemas/ProgrammingWinJS/Controls/Calendar"
    name="ProgWinJS.Controls.Calendar"
    xmlns="http://openajax.org/metadata">

<author name="Kenichiro Tanaka" />
```