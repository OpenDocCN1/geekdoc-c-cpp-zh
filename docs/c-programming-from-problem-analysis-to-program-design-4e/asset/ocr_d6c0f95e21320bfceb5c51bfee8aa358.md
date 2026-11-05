# HTML (.aspx) FILE

Dragging a Web Forms Button object onto a form, setting its ID (name) to btnSubmit, and changing its Text value and positioning properties produces the HTML statement shown in Example 15-7.

# EXAMPLE 15.7

```
```aspx
<asp:Button ID="btnSubmit" runat="server"
    style="z-index: 1; left: 400px; top: 321px;
    position: absolute; width: 90px; height: 24px;
    text-align: center" Text="Submit Info"
    OnClick="btnSubmit_Click" />
```
```

As you can see from Example 15-7, the settings for the properties are not placed in the code-behind file. These attributes are added to the .aspx file—the markup file that contains all the HTML tags. The entries added to the code-behind file (.aspx.cs file) include only the declaration of objects and the registration of event handlers along with their methods.

# CHANGING PROPERTIES WITHIN VISUAL STUDIO

It is valuable to examine the properties that can be set for the buttons, labels, text boxes, radio buttons, check boxes, and other form type controls. As shown in Figure 15-17, there are fewer controls found with Web Forms types of controls than you find with their Windows Forms counterparts. In addition, there are fewer properties for each control and differences exist between the properties. One obvious difference is in naming the object. With Windows Forms controls, the Name property is used. With Web Forms controls, the ID property is used. The following list shows the number of events and controls that can be registered for different types of control buttons:

+   - Windows Forms button—60 events
+   - Web Forms Standard button control—8 events
+   - Windows Forms button control—76 properties
+   - Web Forms Standard button control—36 properties

This comparison is representative of all of the other controls.