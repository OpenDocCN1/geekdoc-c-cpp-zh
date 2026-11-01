```
ErrorMessages="You must enter an event name." ControlToValidate="eventBox" Display="None" />
</td>
</tr>
```

Most of the ASP.NET code in this file is remarkably simple, and much can be learned simply by reading through it. Of particular note in this code is the way in which list items are attached to the controls for selecting a meeting room and multiple attendees for the event:

```
<tr>
  <td valign="top">Meeting Room</td>
  <td valign="top">
    <asp:DropDownList ID="roomList" Runat="server" Width="160px">
      <asp:ListItem Value="1">The Happy Room</asp:ListItem>
      <asp:ListItem Value="2">The Angry Room</asp:ListItem>
      <asp:ListItem Value="3">The Depressing Room</asp:ListItem>
      <asp:ListItem Value="4">The Funked Out Room</asp:ListItem>
    </asp:DropDownList>
    <asp:RequiredFieldValidator ID="validateRoom" Runat="server"
      ErrorMessage="You must select a room."
      ControlToValidate="roomList" Display="None" />
  </td>
</tr>
<tr>
  <td valign="top">Attendees:</td>
  <td valign="top">
    <asp:ListBox ID="attendeeList" Runat="server" Width="160px"
      SelectionMode="Multiple" Rows="5">
      <asp:ListItem Value="1">Bill Gates</asp:ListItem>
      <asp:ListItem Value="2">Monica Lewinsky</asp:ListItem>
      <asp:ListItem Value="3">Vincent Price</asp:ListItem>
      <asp:ListItem Value="4">Vlad the Impaler</asp:ListItem>
      <asp:ListItem Value="5">Iggy Pop</asp:ListItem>
      <asp:ListItem Value="6">William Shakespeare</asp:ListItem>
    </asp:ListBox>
  </td>
</tr>
```

Here you are associating ListItem objects with the two web server controls. These objects are not web server controls in their own right (they simply inherit from System.Object), which is why you don't need to use runat="server" on them. When the page is processed, the <asp:ListItem> entries are used to create ListItem objects, which are added to the Items collection of their parent list control. This makes it easier for you to initialize lists than to write code for this yourself (you would need to create a ListItemCollection object, add ListItem objects, and then pass the collection to the list control). Of course, you can still do this programmatically if you want.

```
<asp:RequiredFieldValidator ID="validateAttendees" Runat="server"
  ErrorMessage="You must have at least one attendee."
  ControlToValidate="attendeeList" Display="None" />
</td>
</tr>
<tr>
  <td align="center" colspan="3">
    <asp:Button ID="submitButton" Runat="server" Width="100%"
      Text="Submit meeting room request" />
  </td>
</tr>
<tr>
```