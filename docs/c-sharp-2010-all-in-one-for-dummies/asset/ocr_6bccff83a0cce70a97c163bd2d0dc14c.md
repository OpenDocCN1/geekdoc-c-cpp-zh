```
1 - The TextBox<br />
<asp:TextBox ID="TextBox1" runat="server">The TextBox</asp:TextBox>
<br />
<br />
2. The TextArea<br />
<asp:TextBox ID="TextBox2" runat="server" TextMode="MultiLine">The TextArea</asp:TextBox>
<br />
<br />
3. The Password<br />
<asp:TextBox ID="TextBox3" runat="server" TextMode="Password">The Password</asp:TextBox>

</div>
</form>
</body>
</html>
```

In order to set properties in the C# code, I would refer to the ID, as set in the property panel. If you use the defaults (don't do this in real code, make real names for controls), configuring the first text box might look something like this:

```
public partial class WebForm1 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        TextBox1.MaxLength = 20;
        TextBox1.Height = 22;
        TextBox1.Width = 135;
        TextBox1.Enabled = true;
    }
}
```

# Using single-item selection controls

After collecting text, the next most common user-input gathering operation is asking them to choose an item from a list. In HTML, you can do this with check boxes, radio buttons, or drop-down lists. (See Figure 3-3.)

Figure 3-3:
The single selectors.

![](bbox=[0.27, 0.8, 0.88, 0.97])