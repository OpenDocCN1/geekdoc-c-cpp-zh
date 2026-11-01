Each control must display a context menu. Several menu choices will be available for all of the controls, but each control will also have a couple of unique menu choices. The common choices can be defined on one ContextMenuStrip. Each of the unique menu items can be predefined or created at runtime. For each control that needs a context menu assigned to it, the common menu is cloned and the unique choices are merged with the common menu using the ToolStripManager.Merge method. The resulting menu is assigned to the ContextMenuStrip property of the control.

# ToolStripContainer

The ToolStripContainer control is used for docking of ToolStrip-based controls. When you add a ToolStripContainer and set the Docked property to Fill, a ToolStripPanel is added to each side of the form, and a ToolStripContainerPanel is added to middle of the form. Any ToolStrip (ToolStrip, MenuStrip, or StatusStrip) can be added to any of the ToolStripPanels. The user can move a ToolStrip by grabbing it and dragging it to either side or bottom of the form. If you set the Visible property to false on any of the ToolStripPanels, a ToolStrip can no longer be placed in the panel. The ToolStripContainerPanel in the center of the form can be used to place the other controls the form may need.

# FORMS

Earlier in this chapter, you learned how to create a simple Windows application. The example contained one class derived from the System.Windows.Forms.Form class. According to the .NET Framework documentation, “A form is a representation of any window in your application.” If you come from a Visual Basic background, the term “form” will seem familiar. If your background is C++ using MFC, you’re probably used to calling a form a window, dialog box, or maybe a frame. Regardless, the form is the basic means of interacting with the user. Earlier, the chapter covered some of the more common and useful properties, methods, and events of the Control class, and because the Form class is a descendant of the Control class, all of the same properties, methods, and events exist in the Form class. The Form class adds considerable functionality to what the Control class provides, and that’s what this section discusses.

# Form Class

A Windows client application can contain one form or hundreds of forms. The forms can be an SDI-based (Single Document Interface) or MDI-based (Multiple Document Interface) application. Regardless, the System.Windows.Forms.Form class is the heart of the Windows client. The Form class is derived from ContainerControl, which is derived from ScrollableControl, which is derived from Control. Because of this, you can assume that a form is capable of being a container for other controls, is capable of scrolling when the contained controls do not fit the client area, and has many of the same properties, methods, and events that other controls have. This also makes the Form class rather complex. This section looks at much of that functionality.

# Form Instantiation and Destruction

The process of form creation is important to understand. What you want to do depends on where you write the initialization code. For instantiation, the events occur in the following order:

+   - Constructor
+   - Load
+   - Activated
+   - Closing
+   - Closed
+   - Deactivate