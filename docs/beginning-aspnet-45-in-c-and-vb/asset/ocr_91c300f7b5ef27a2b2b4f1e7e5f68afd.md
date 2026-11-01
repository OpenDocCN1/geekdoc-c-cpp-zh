(continued)

| PROPERTY | DESCRIPTION |
|---|---|
| CssClass | Enables you to define the HTML class attribute for the control in the browser. This class name could then point to a CSS class you defined in the page or an external CSS file. |
| Enabled | Determines whether the user can interact with the control in the browser. For example, with a disabled text box (Enabled="False") you cannot change its text. |
| Font | Enables you to define different font-related settings, such as size, family and whether or not the font should be bold. |
| Height Width | Determines the height and width of the control in the browser. |
| TabIndex | Sets the client-side HTML tabindex attribute that determines the order in which users can move through the controls in the page by pressing the Tab key. |
| ToolTip | Enables you to set a tooltip for the control in the browser. This tooltip, rendered as a title attribute in the HTML, is shown when the user hovers the mouse over the element. |
| Visible | Determines whether or not the control is sent to the browser. You should really see this as a server-side visibility setting because an invisible control is never sent to the browser at all. This means it's quite different from the CSS display and visibility properties you saw in the previous chapter that hide the element at the client. |

To see how all these attributes end up in the browser, consider the following markup for a TextBox server control:

```
<asp:TextBox AccessKey="a" BackColor="Black" ForeColor="White" Font-Size="30px" BorderColor="Yellow" BorderStyle="Dashed" BorderWidth="4" CssClass="TextBox" Enabled="True" Height="40" Width="200" TabIndex="1" ToolTip="Hover text here" Visible="True" ID="TextBox1" runat="server" Text="Hello World"> </asp:TextBox>
```

When you request the page with this control in the browser, you end up with the following HTML:

```
<input name="TextBox1" type="text" value="Hello World" id="TextBox1" accesskey="a" tabindex="1" title="Hover text here" class="TextBox" style="color:White; background-color:Black;border-color:Yellow;border-width:4px; border-style:Dashed;font-size:30px;height:40px;width:200px;" />
```

This results in the text box shown in Figure 4-3.