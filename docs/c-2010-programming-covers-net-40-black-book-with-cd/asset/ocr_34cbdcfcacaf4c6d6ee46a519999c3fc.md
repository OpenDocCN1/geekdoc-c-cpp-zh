```
<tr>
    <td>
        Password Question:</td>
    <td class="style1">
        <asp:DropDownList ID="dropdownlist1" Runat="server" Width="100%">
            <asp:ListItem>Your favorite place?</asp:ListItem>
            <asp:ListItem>Your favorite color?</asp:ListItem>
            <asp:ListItem>Your role model?</asp:ListItem>
        </asp:DropDownList>
    </td>
</tr>
<tr>
    <td>
        Password Answer:</td>
    <td class="style1">
        <asp:textbox id="myPasswordAnswer" runat="server" width="92%"></asp:textbox>
    </td>
</tr>
<tr>
    <td style="TEXT-ALIGN: center" colspan="2">
        <asp:Button ID="createbutton" runat="server" text="Click to Create User" onclick="createbutton_Click"/>
    </td>
</tr>
</table>
<br />
<br />
<asp:Label ID="lblresults" runat="server" Visible="false">Results:</asp:Label>
</div>
</form>
</body>
</html>
```

3. Add the code, given in Listing 36.23, in the code-behind file of the Default.aspx page to add the functionality of creating user using the Membership class:

# Listing 36.23: Showing the Code for the Code-Behind File of the Default.aspx Page

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Web.Security;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
    }
    protected void createbutton_Click(object sender, EventArgs e)
    {
        MembershipCreateStatus status;
        Membership.CreateUser(myUserId.Text, myPassword.Text, myEmail.Text, dropdownlist1.SelectedValue, myPasswordAnswer.Text, true, out status);
        switch (status)
        {
            case (MembershipCreateStatus.Success):
                myUserId.Text = null;
                myPassword.Text = null;
                myEmail.Text = null;
                dropdownlist1.SelectedIndex = -1;
                myPasswordAnswer.Text = null;
                lblresults.Text = "User successfully created!";
                break;
            case (MembershipCreateStatus.DuplicateUserName):
```