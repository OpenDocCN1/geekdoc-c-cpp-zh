![](bbox=[0.175, 0.098, 0.59, 0.51])

> > You can mix and match HTML controls, HTML server controls, and Web Forms Standard controls. A single Web application can contain all three.

Web Forms controls do not map straight to HTML. Often it may take several HTML tags to represent one Web Forms control. When you drag and drop a Web Forms control onto the page, an HTML tag is placed in the .aspx file representing the control. This tag contains an extra attribute, which is not found on HTML controls, as follows:

```
```html
<asp:controlName> attributes runat="server"
</asp:controlName>
```
```

To indicate that the control is a Web Forms control, Visual Studio prefixes the control name with <asp:controlName> and ends the tag with </asp:controlName>.You saw runat="server" previously. This attribute is added for Web Forms controls.