to 3.5 this ClientID was always generated for you automatically. However, in ASP.NET 4 new ClientMode property was introduced that gives you more control over the ID of an element at the client. You will see how this works in later chapters. The runat attribute is technically not a property of a server control, but is necessary to identify that the mark for the control should be processed as a server control and not end up as plaintext or HTML in the browser.

Besides these properties, many of the server controls share more properties because they share the same Control base class. The next chapter goes deeper into base classes and inheritance. following table lists the most common shared properties and describes what they are used for.

| PROPERTY | DESCRIPTION |
| --- | --- |
| AccessKey | Enables you to set a key with which a control can be accessed at the client by pressing the associated key on the keyboard. |
| BackColor ForeColor | Enables you to change the color of the background (BackColor) and text (ForeColor) of the control. |
| BorderRadius BorderWidth | Changes the border of the control in the browser. The similarities with the CSS border properties you saw in the previous chapter are no coincidence. Each of these three ASP.NET properties maps directly to its CSS counterpart. |
| CssClass | Enables you to define the HTML class attribute for the control in the browser. This class name then point to a CSS class you defined in the page or an external CSS file. |
| Enabled | Determines whether the user can interact with the control in the browser. For example, with a disabled text box (Enabled="False") you cannot change its text. |
| Font | Enables you to define different font-related settings, such as size, family and whether or not the font should be bold |
| Height Width | Determines the height and width of the control in the browser. |
| TabIndex | Sets the client-side HTML tabindex attribute that determines the order in which users can move through the controls in the page by pressing the Tab key. |
| ToolTip | Enables you to set a tooltip for the control in the browser. This tooltip, rendered as a title attribute in the HTML, is shown when the user hovers over the element. |
| Visible | Determines whether or not the control is sent to the browser. You should really see this as a server-side visibility setting because an invisible control is never sent to the browser at all. This means it's quite different from the CSS display and visibility properties you saw in the previous chapter that hide the element at the client.