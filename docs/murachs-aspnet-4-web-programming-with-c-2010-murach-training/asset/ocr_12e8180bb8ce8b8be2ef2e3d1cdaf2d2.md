# An UpdateProgress control in Design view

![](bbox=[0.124, 0.108, 0.824, 0.432])

# Three attributes of the UpdateProgress control

| Attribute | Description |
|---|---|
| DynamicLayout | Determines whether space is allocated on the page for the content of the control when it isn’t displayed. The default is True, which means that space is dynamically allocated. If set to False, space is allocated for the content even though it won’t be seen until an asynchronous postback occurs. |
| DisplayAfter | Determines how long in milliseconds after the asynchronous postback has started to display the content. The default is 500 milliseconds (0.5 seconds). This value can prevent the content from flickering when the postback happens quickly. |
| AssociatedUpdatePanelID | The ID of the UpdatePanel control that the control is associated with. |

# The aspx code for an UpdatePanel control with an UpdateProgress control

```
```aspx
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
    <ContentTemplate>
        <asp:UpdateProgress ID="UpdateProgress1" runat="server">
            <ProgressTemplate>
                Please wait. The update is in progress.
            </ProgressTemplate>
        </asp:UpdateProgress>
    </ContentTemplate>
</asp:UpdatePanel>
```
```

# Description

+   - An UpdateProgress control must contain a ProgressTemplate element that defines the content of the control. This content is displayed only while an asynchronous postback is in progress. It is hidden after the asynchronous postback is complete.

Figure 21-10   How to use the UpdateProgress control