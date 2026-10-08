
# LISTING 20-18: CustomEditor.cs

![](img/b5597c749e848b27b0d305153ae16106_978_0.png)

```c
using AjaxControlToolkit.HTMLEditor;
using ToolbarButton = AjaxControlToolkit.HTMLEditor.ToolbarButton;

namespace ActControlSamples
{
    public class CustomEditor : Editor
    {
        protected override void FillTopToolbar()
        {
            TopToolbar.Buttons.Add(new ToolbarButton.Undo());
            TopToolbar.Buttons.Add(new ToolbarButton.Redo());
            TopToolbar.Buttons.Add(new ToolbarButton.HorizontalSeparator());
            TopToolbar.Buttons.Add(new ToolbarButton.Bold());
            TopToolbar.Buttons.Add(new ToolbarButton.Italic());
            TopToolbar.Buttons.Add(new ToolbarButton.Underline());
            TopToolbar.Buttons.Add(new ToolbarButton.StrikeThrough());
            TopToolbar.Buttons.Add(new ToolbarButton.SubScript());
            TopToolbar.Buttons.Add(new ToolbarButton.SuperScript());
            TopToolbar.Buttons.Add(new ToolbarButton.HorizontalSeparator());
            TopToolbar.Buttons.Add(new ToolbarButton.Cut());
            TopToolbar.Buttons.Add(new ToolbarButton.Copy());
            TopToolbar.Buttons.Add(new ToolbarButton.PasteText());
        }

        protected override void FillBottomToolbar()
        {
        }
    }
}
```

> Code file [CustomEditor.cs] available for download at Wrox.com

![](img/b5597c749e848b27b0d305153ae16106_978_1.png)

The AjaxControlToolkit.HTMLEditor.Toolbar class has several nested classes representing editor buttons on the toolbar. With overriding the FillTopToolbar and FillBottomToolbar methods, you can define your own buttons — and so you can constrain the functionality of your editor.

The CustomEditor class keeps the bottom toolbar empty, and allows you to use only the design edit panel. The top toolbar contains only formatting buttons. Figure 20-17 shows this custom editor in action.

FIGURE 20-17: Customized Editor in action

# Control Extenders

A majority of controls in the Ajax Control Toolkit are extenders. They cannot be used as individual controls. They are always attached to another ASP.NET control to add value by extending that control's behavior. This section examines almost all controls in the Toolkit.

All extenders have a TargetID property that can be used to identify the control to which the extender is attached. Consider the following example:

```asp
<asp:Button ID="DisableButton" runat="server"
Text="Disable this CheckBox"
OnClick="DisableButton_Click" />
<asp:ConfirmButtonExtender ID="ConfirmButtonExtender1" runat="server"
TargetControlID="DisableButton"
ConfirmText="Are you sure you want to do that?" />
```

This structure implicitly tells you an extender can have exactly one control to which it is attached. A control may have zero, one, or more extenders extending it.

> Most of extenders have many more properties than introduced and demonstrated in this section's. For a complete reference of properties visit the Ajax Control Toolkit site (http://www.asp.net/ajax/ajaxcontroltoolkit/samples).

# Button and Checkbox Extenders

Two extenders can examine Checkbox controls:

- ToggleButtonExtender enables the use of custom images to show the state of the CheckBox without affecting the CheckBox's behavior.
- MutuallyExclusiveCheckBoxExtender, You can add a number of checkboxes to the same "Key", and only one CheckBox with the specified key can be checked at a time.

The third control, ConfirmButtonExtender, catches on a click (or on any instance of a type that is derived from Button, such as a LinkButton) and displays a message to the user. If the user clicks OK, or the button functions normally.

The ButtonExtendersSample.aspx page in the sample project demonstrates these concepts. Figure 20-18 shows the example in action.

Each checkbox in the page has an attached ToggleButtonExtender. A ConfirmButtonExtender close to the top of the page enables or disables

![](img/b5597c749e848b27b0d305153ae16106_779_0.png)

FIGURE 20-18: ButtonExtendersSample.aspx in action

the checkbox on its left side. The six checkboxes at the bottom part form two groups with attached MutuallyExclusiveCheckBoxExtender instances. All controls in the page are wrapped with an UpdatePanel. The code below the UI part above the horizontal bar is in Listing 20-19.

# LISTING 20-19: ButtonExtendersSample.aspx (Code Extract, Part 1)

```asp
<asp:CheckBox Id="Checkbox" Checked="true"
    Text="Click me to ToggleButtonExtender!"
    runat="server" />
<asp:ToggleButtonExtender Id="ToggleExt1" runat="server"
    TargetControl="Checkbox"
Width="16" Height="16"
CheckedImageUrl="Images/Checked.png"
CheckedImageOverUrl="Images/Checked-Hovered.png"
DisabledCheckedOverUrl="Images/Checked-Disabled.png"
CheckedImageAlternateText="Checked"
UncheckedImageUrl="Images/Unchecked.png"
UncheckedImageOverUrl="Images/Unchecked-Hovered.png"
DisabledUncheckedOverUrl="Images/Unchecked-Disabled.png"
UncheckedImageAlternateText="Unchecked" />
<asp:CheckBox Id="Checkbox2" Checked="true"
    Text="Try me to ToggleButtonExtender!"
    runat="server" />
<asp:ToggleButtonExtender Id="ToggleExt2" runat="server"
    TargetControl="Checkbox2"
Width="16" Height="16"
CheckedImageUrl="Images/Checked.png"
CheckedImageOverUrl="Images/Checked-Hovered.png"
DisabledCheckedOverUrl="Images/Checked-Disabled.png"
CheckedImageAlternateText="Checked"
UncheckedImageUrl="Images/Unchecked.png"
UncheckedImageOverUrl="Images/Unchecked-Hovered.png"
DisabledUncheckedOverUrl="Images/Unchecked-Disabled.png"
UncheckedImageAlternateText="Unchecked" />
<asp:Button Id="DisableButton" runat="server"
    Text="DisableButton, Click" />
<asp:ConfirmButtonExtender ID="ConfirmButtonExtender1" runat="server"
    TargetControlID="DisableButton"
ConfirmText="Are you sure you want to do that?"
ConfirmSubmit="true" />
```

Code file [ButtonExtendersSample.aspx] available for download at Wrox.com.

As you see, you can define CheckBox state. Unfortunately, when you want to declare more ToggleButtonExtender instances, you must set the image-related properties for each extender. The definition of ConfirmButtonExtender is much shorter. You can also define the ImageHeight and ImageWidth, of the image that will be displayed. You will learn about this in this chapter. The code defining the checkboxes at the bottom of the page forming the Color and Size groups is shown in Listing 20-20.

# LISTING 20-20: ButtonExtendersSample.aspx (Code Extract, Part 2)

```asp
<table>
  <tr>
    <td valign="top">Select Color:</td>
    <td>
      <asp:Panel ID="ColorPanel" runat="server">
        <asp:CheckBox ID="Red" runat="server" Text="Red" />
        <asp:MutuallyExclusiveCheckBoxExtender
          ID="MutExt1" runat="server" TargetControlID="Red"
          Key="Color" />
        <br />
        <asp:CheckBox ID="Green" runat="server" Text="Green" />
        <asp:MutuallyExclusiveCheckBoxExtender
          ID="MutExt2" runat="server" TargetControlID="Green"
          Key="Color" />
        <br />
        <asp:CheckBox ID="Blue" runat="server" Text="Blue" />
        <asp:MutuallyExclusiveCheckBoxExtender
          ID="MutExt3" runat="server" TargetControlID="Blue"
          Key="Color" />
      </asp:Panel>
    </td>
  </tr>
  <tr>
    <td valign="top">Select Size:</td>
    <td>
      <asp:Panel ID="SizePanel" runat="server">
        <asp:CheckBox ID="Small" runat="server" Text="Small" />
        <asp:MutuallyExclusiveCheckBoxExtender
          ID="MutExt4" runat="server" TargetControlID="Small"
          Key="Size" />
        <br />
        <asp:CheckBox ID="Medium" runat="server" Text="Medium" />
        <asp:MutuallyExclusiveCheckBoxExtender
          ID="MutExt5" runat="server" TargetControlID="Medium"
          Key="Size" />
        <br />
        <asp:CheckBox ID="Large" runat="server" Text="Large" />
        <asp:MutuallyExclusiveCheckBoxExtender
          ID="MutExt6" runat="server" TargetControlID="Large"
          Key="Size" />
      </asp:Panel>
    </td>
  </tr>
</table>
```
