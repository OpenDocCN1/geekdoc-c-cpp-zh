```
~~~javascript
function captureSelection() {
    var source = document.getElementById("webviewSource");

    //wrap the capture method in a promise
    var promise = new WinJS.Promise(function (cd, ed) {
        var op = source.captureSelectedContentToDataPackageAsync();
        op.oncomplete = function (args) { cd(args.target.result); };
        op.onerror = function (e) { ed(e); };
        op.start();
    });

    //Navigate the output webview to the selection, or show an error
    var output = document.getElementById("webviewOutput");

    promise.then(function (dataPackage) {
        if (dataPackage == null) { throw "No selection"; }

        var view = dataPackage.getView();
        return view.getHtmlFormatAsync();
    }).done(function (text) {
        output.navigateToString(text);
    }, function (e) {
        output.navigateToString("Error: " + e.message);
    });
}
~~~
```

The output of this example is shown in Figure 4-3. On the left is a webview-hosted page (my blog), and on the right is the captured selection. Note that the captured selection is an HTML clipboard format that includes the extra information at the top before the HTML from the webview. If you need to extract just the straight HTML, you'll need to strip off this prefix text up to <!DOCTYPE html>.

Generally speaking, captureSelectedContentToDataPackageAsync will produce the formats AnsText, Text, HTML Format, Rich Text Format, and msSourceUrl, but not a bitmap. For this you need to use the third method, capturePreviewToBlobAsync, which again has a start method and complete/error events. The results of this capture (in args.target.result within the complete handler) is a blob object for whatever content is contained within the webview's display area.

![](bbox=[0.143, 0.698, 0.791, 0.87])

FIGURE 4-3 Example output from the WebviewExtras example, showing that the captured selection from a webview includes information about the selection as well as the HTML itself.