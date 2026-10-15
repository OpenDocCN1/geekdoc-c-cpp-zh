| Table 14.10: Noteworthy Public Properties of the Label Class |
| Property | Description |
| Text | Obtains or sets the text to be displayed in the Label control |
| Width | Specifies the width of the Label control |

# The HyperLink Control

The HyperLink control is used to create a link to another Web page that can be a page in your Web application or anywhere else on the World Wide Web (WWW). The HyperLink control exists within the System.Web.UI.WebControls namespace. The inheritance hierarchy for the HyperLink class is as follows:

```
System.Object
System.Web.UI.Control
System.Web.UI.WebControls.WebControl
System.Web.UI.WebControls.HyperLink
```

You can specify the location of the linked page by specifying its URL on the current page. You can use text as well as image in the HyperLink control. Text is specified with the Text property and image is specified by the ImageUrl property. By default, when you click a HyperLink control, the hyperlinked content appears in a new browser window. You can set the Target property to the name of a window or frame, as listed in Table 14.11:

| Table 14.11: Target Property Options of the HyperLink Class |
| Property | Description |
| _blank | Displays the hyperlinked content in a new window without frames |
| _parent | Displays the hyperlinked content in the immediate frameset parent |
| _self | Displays the hyperlinked content in the frame with focus |
| _top | Displays the hyperlinked content in the full window without frames |

The HyperLink class has no non-inherited method or event. Noteworthy public properties of the HyperLink class are listed in Table 14.12:

| Table 14.12: Noteworthy Public Properties of the HyperLink Class |
| Property | Description |
| ImageUrl | Obtains the path to an image to be displayed for the HyperLink control |
| NavigateUrl | Obtains the URL to link to a Web page when the HyperLink control is clicked |
| Target | Obtains the target window to display the Web page data when the HyperLink control is clicked |
| Text | Obtains the text caption for the HyperLink control |

# The HiddenField Control

The HiddenField control is used to store a value that needs to persist across posts to the server. Normally, view-state, session-state, and cookies are used to maintain the state of a Web page. In case, if these methods are disabled or are not available, you can use the HiddenField control to store state values. The class hierarchy for the HiddenField class is as follows:

```
System.Object
System.Web.UI.Control
System.Web.UI.WebControls.HiddenField
```

Table 14.13 lists the noteworthy public properties of the HiddenField class:

| Table 14.13: Public Properties of the HiddenField Class |
| Property | Description |
| EnableTheming | Obtains or sets a value indicating whether or not themes apply to the HiddenField control |