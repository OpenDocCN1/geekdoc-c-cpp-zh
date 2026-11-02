Invoking script in a webview is demonstrated in scenario 5 of the HTML WebView control sample, where the following content of html/script_example.html (condensed here) is loaded into the webview:

```
<!DOCTYPE html><html><head>
<title>Script Example</title>
<script type="text/javascript">
function changeText(text) {
    document.getElementById("myDiv").innerText = text;
}
</script>
</head><body>
<div id="myDiv">Call the changeText function to change this text</div>
</body></html>
```

The app calls changeText as follows:

```
document.getElementById("webview").invokeScriptAsync("changeText", document.getElementById("textInput").value).start();
```

The second parameter to invokeScriptAsync method is always a string (or will be converted to a string). If you want to pass multiple arguments, use JSON.stringify on an object with suitably named properties and JSON.parse it on the other end.

Take note! Notice the all-important start() tacked onto the end of the invokeScriptAsync call. This is necessary to actually run the async calling operation. Without it, you'll be left wondering just why exactly the call didn't happen! We'll talk more of this in a moment with another example.

Receiving an event from a webview is demonstrated in scenario 6 of the sample. An event is raised using the window.external.notify method, whose single argument is again a string. In the sample, the html/scriptnotify_example.html page contains this bit of JavaScript:

```
window.external.notify("The current time is " + new Date());
```

which is picked up in the app as follows, where the event arg's value property contains the arguments from window.external.notify:

```
document.getElementById("webview").addEventListener("MSWebViewScriptNotify", scriptNotify);

function scriptNotify(e) {
  var outputArea = document.getElementById("outputArea");
  outputArea.value += ("ScriptNotify event received with data:\n" + e.value + "\n\n");
  outputArea.scrollTop = outputArea.scrollHeight;
}
```

Requirement MSWebViewScriptNotify will be raised only from webviews loaded with ms-appx-web, ms-local-stream, and https content, where https also requires a content URI rule in your manifest, otherwise that event will be blocked. ms-appdata is also allowed if you have a URI resolver involved. Note that a webview loaded through navigateToString does not have this requirement.