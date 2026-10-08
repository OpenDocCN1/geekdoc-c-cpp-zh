# TABLE 19-1: Available Split Script Files

| SCRIPT FILE NAME | SYS.SCRIPTS VALUE |
|--- |--- |
| MicrosoftAjaxAdoNet.js | AdoNet |
| MicrosoftAjaxApplicationServices.js | ApplicationServices |
| MicrosoftAjaxComponentModel.js | ComponentModel |
| MicrosoftAjaxCore.js | Core |
| MicrosoftAjaxDataContext.js | DataContext |
| MicrosoftAjaxGlobalization.js | Globalization |
| MicrosoftAjaxHistory.js | History |
| MicrosoftAjaxNetwork.js | Network |
| MicrosoftAjaxSerialization.js | Serialization |
| MicrosoftAjaxTemplates.js | Templates |
| MicrosoftAjaxWebServices.js | WebServices |
| jquery-1.3.2.min.js | jQuery |
| jquery.validate.min.js | jQueryValidate |

Features may also include components. For example, if you use the DataView and the Watermark components on the page, you do not have to know which scripts they contain. You just load them via a single Sys.require call:

```
Sys.require([Sys.components.dataView, Sys.components.watermark]);
```

Because the Sys.require function loads scripts asynchronously, you may find the second parameter useful, which is a callback that is called when all the features are available.

The Script Loader relies on metadata about every feature defined in the Start.js file via the Sys.loader.defineScripts method. Because you can also use this method to describe your custom script files, it is worth taking a look at how Microsoft did it (code fragment from Start.js):

```
loader.defineScripts(
{
  releaseUrl: "%MicrosoftAjax" + {0}.js",
  debugUrl: "%MicrosoftAjax" + {0}.debug.js",
  executionDependencies: ["Core],
  {
    name: "Core",
    executionDependencies: null,
    isLoaded: !!window.Type
```