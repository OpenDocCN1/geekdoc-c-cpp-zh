individual files. This script-combining feature is managed automatically by the Loader; all you have to do is describe the composite scripts with the contains property for your custom scripts.

Note the following two things with script combining:

+   - The Script Loader is a client-side component. It can download only what is already available on the server. It is your responsibility to combine and publish the composite scripts on the server.

+   - The Loader loads the composite script file only if all the scripts that it contains are required on the page, and only if you load them with a single Sys.require call.

You can use composite scripts and single scripts mixed in a page. If you have a single Sys.require call with the seven components mentioned earlier, the jQuery Library, the Loader will download the composite script with a single HTTP request, and the jQuery Library with another request.

The Script Loader also supports loading scripts on demand. You can use the script tag or Sys.require calls to load the scripts required by most of users at page time, and delay loading those scripts that are required for specific features and a smaller number of users. For example, if you have a Print button on the page, you can use its event handler to download the script files required for the print functionality with the Sys.loader.loadScripts function. This will definitely cause a small delay for those who click the Print button (only the first time, because the browser will cache the script), but will provide better page load time for all users.

As you have already realized, the Script Loader is a really smart component. It supports script dependencies, composite scripts, parallel download, lazy loading, the Microsoft Ajax CDN, and so on. All the features of the Script Loader are available not only for the Microsoft Ajax Library and the jQuery Library, but also for your custom scripts. However, if you want to integrate your own scripts, you should take a look at the Sys.loader.registerScript function, and the recommended implementation pattern that follows this architecture.

# Client-Side Data Binding with Templates

Let's suppose you have an object array, and your task is to display the objects in an unordered list on the page. For this example, let's consider an array of country data in a variable named countries. You can fill this array from the server or initialize it locally:

```
var countries = [
  { Name: 'Austria', Code: 'at', Capital: 'Vienna' },
  { Name: 'Hungary', Code: 'hu', Capital: 'Budapest' },
  { Name: 'United States', Code: 'us', Capital: 'Washington, D.C.' },
  //
];
```

![](bbox=[0.95, 0.745, 0.15, 0.81])

> Code file [3-AjaxLibrary03-CodeAndMarkup.htm] available for download at Wrox.com.

You can also have a set of image files that are named by the country code and the flags of the countries. To complete the task, you must render HTML markup of the unordered list