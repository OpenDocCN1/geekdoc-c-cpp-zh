the implementation is entirely different.

In Android, a prompt is shown so you can select which app it should use to send the Intent. Or, if you have one already set as default, it will automatically open it and load the article you’ve clicked on. MainActivity.kt, in androidApp/ui, defines this function:

```
```
private fun openEntry(url: String) {
  val intent = Intent(Intent.ACTION_VIEW)
  intent.data = Uri.parse(url)
  startActivity(intent)
}
```
```

Since anyone can have multiple apps installed on a device, it’s important to define which apps are capable of receiving this intent. In this scenario, you’re looking for apps that can open a URL. To avoid opening the wrong app, Android allows you to define a couple of parameters the system uses to filter between all installed apps, and the one that best fit your Intent. First, it checks for those that have on their AndroidManifest.xml the ACTION_VIEW attribute defined, and then those that are capable to parse URIs.

iOS has a different approach. To open a URL, you just need to use the OpenURLAction from the environment. Open LatestView.swift from iosApp module and scroll to the Section struct:

```
```
@Environment(\..openURL) var openURL
```
```

The var openURL allows you to send a URL that will open the default browser on your device:

```
```
openURL(URL(string: "\\\(item.link)")!)
```
```

When the user clicks on one of the articles, the app creates a URL from that item link and calls openURL with it to open the link in the browser.

desktopApp uses another approach. Desktop has a browser function that you can use to launch the default browser on your computer. Open the Main.kt from the desktopApp module and scroll down to the end of this file:

```
```
fun openEntry(url: String) {
  try {
    val desktop = Desktop.getDesktop()
    desktop.browse(URI.create(url))
  } catch(e: Exception) {
    Logger.e(TAG, "Unable to open url. Reason: ${e.stackTrace}")
  }
}
```
```