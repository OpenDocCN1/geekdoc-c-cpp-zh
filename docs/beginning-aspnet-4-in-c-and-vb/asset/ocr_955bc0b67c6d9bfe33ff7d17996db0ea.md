You also need to add the following event handler to the code behind this file:

```
```csharp
protected void OnSelect(object sender, EventArgs e)
{
    favoriteColorLabel.Text = ((LinkButton)sender).Text;
    favoriteColorLabel.Style["color"] = ((LinkButton)sender).Style["color"];
}
```
```

*code snippet PCSExtenderDemo/Default.aspx.cs*

In the browser, not very much is visible at first, and the extender seems to have no effect. This is shown in Figure 41-16.

![](bbox=[0.15, 0.39, 0.65, 0.51])

FIGURE 41-16

However, when you hover over the text that reads "green," a drop-down dynamically appears. If you click this drop-down, a list appears, as shown in Figure 41-17.

![](bbox=[0.15, 0.65, 0.6, 0.79])

FIGURE 41-17

When you click one of the links in the drop-down list, the text changes accordingly (after a partial-page postback operation).

There are two important points to note about this simple example:

+   - It was extremely easy to associate the extender with target controls.
+   - The drop-down list was styled using custom code — meaning that you can place whatever content you like in the list. This simple extender is a great way to add functionality to your web applications, and it is very simple to use.

The extenders that are contained in the AJAX Control Toolkit are continually being added to and updated, so check http://www.asp.net/ajax/AjaxControlToolkit/Samples/ regularly. This web page includes live demonstrations of all the current extenders so that you can see them in action.

In addition to the extender controls that are supplied by the AJAX Control Toolkit, you can create your own. To create an effective extender, you must use the AJAX Library.