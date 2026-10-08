The EditorSample.aspx page of the sample project provides an example of using the Editor control. You can edit within the editor, and by clicking the Submit button, you can post it back to display the content on the page. Figure 20-16 shows this example in action.

![](bbox=[0.143, 0.193, 0.725, 0.618])

FIGURE 20-16: EditorSample.aspx in action

Although you can create a complex UI with toolbars and lists of buttons, the source code declaring the page is really simple, as shown in Listing 20-16.

# LISTING 20-16: EditorSample.aspx

```
<% Language="C#" AutoEventWireup="true" CodeBehind="EditorSample.aspx.cs"
Inherits="ActControlSamples.EditorSample %>
<% Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit.HTMLEditor"
TagPrefix="ajax" %>
<% Register Assembly="AjaxControlToolkit" Namespace="AjaxControlToolkit"
TagPrefix="ajax" %>
```

continues