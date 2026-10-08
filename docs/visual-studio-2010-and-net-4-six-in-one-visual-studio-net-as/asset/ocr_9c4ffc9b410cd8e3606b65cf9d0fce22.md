The control has several properties not examined here, yet which are also very useful when customizing the Accordion control. Table 20-5 describes them.

**TABLE 20-5:** Accordion Properties

| PROPERTY | DESCRIPTION |
| --- | --- |
| AutoSize | This value specifies how to restrict the layout of the Accordion control: None — The control grows and shrinks without restriction. Limit — The Accordion never grows larger than the value specified by its Height. This property causes the content to scroll if the content is too long to be displayed in the allotted space. Fill — The content is a fixed size, as specified in its Height property. This allows the content to expand or shrink if the content does not fit exactly into the allotted space. | RequireOpenedPane | This value specifies whether the currently opened pane does not close when its header is clicked (which ensures one pane is always open). The default is true. | SuppressHeaderPostbacks | This flag specifies whether the client-side click handlers of elements are inside a header. This is useful when you want to include hyperlinks in the headers for accessibility. |

# ## The AsyncFileUploadControl

The standard .NET FileUpload control does not work within an Ajax UpdatePanel. If you want to place it in an update panel, then a postback is also required to upload the file. The Toolkit's AsyncFileUploadcontrol allows you to upload the file in an asynchronous manner, and it works with UpdatePanel. A great advantage of this control is that it uploads the file without postback, and provides client-side and server-side events.

The control provides different coloring for file uploads. It can have a green background when the file is uploaded successfully and a red one when upload fails. You can also show a "progress" image while file uploading is in progress.

You can find the AsyncFileUploadSample.aspx in the ControlSamples project to examine how this control works. This project contains client-side scripts, as shown in Listing 20-14.

**LISTING 20-14:** AsyncFileUploadSample.aspx

```
<%@ Language="C#" AutoEventWireup="true"
CodeBehind="AsyncFileUploadSample.aspx.cs"
Inherits="ControlSamples.AsyncFileUploadSample" %>
```

![](bbox=[0.0265, 0.85335, 0.0865, 0.89335])