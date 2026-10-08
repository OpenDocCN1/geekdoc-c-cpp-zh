```
{
  protected void Page_Load(object sender, EventArgs e)
}
```

```
protected void SubmitButton_Click(object sender, EventArgs e)
  EditorContentLiteral.Text = EditorContent;
  var changed = Session["EditorContentChanged"];
  if (changed != null)
    ChangedLabel.Visible = (bool)changed;
  Session["EditorContentChanged"] = false;
}
```

```
protected void Editor1_ContentChanged(object sender, EventArgs e)
  Session["EditorContentChanged"] = true;
```

Code file |EditorSample.aspx| available for download at Wix.com.

The control does not need any initialization, the Page_Load method is empty. Both the SubmitButton_Click and the Editor1_ContentChanged methods are fired when the page is posted back as a result of clicking the Submit button. First, the Editor1_ContentChanged runs then SubmitButton_Click.

The HTML content of the editor is accessed through the Content property. Because it is an HTML string, you can directly assign it to the Text property of the EditorContentLiteral control. The Session stores whether or not the content was changed from the last submit, and ChangedLabel visibility is effectively controllable.

Table 20-7 summarizes the properties you can use with the Editor control.

| PROPERTY | DESCRIPTION |
|---|---|n| ActiveMode | Sets the active editing panel (Design, Html, Preview) to use when the control is loaded. The default is Design. |
| AutoFocus | If this flag is set to true, the editing panel is focused and the cursor is set inside (Design or HTML view) on initial load or editing panel change. |
| Content | Gets or sets the HTML content of the Editor. |
| CssClass | A CSS class override is used to define a custom look and feel for the Editor. |