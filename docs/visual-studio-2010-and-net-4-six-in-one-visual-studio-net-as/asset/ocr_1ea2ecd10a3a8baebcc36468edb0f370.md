```
}
  protected void TabContainer1_ActiveTabChanged(object sender, EventArgs)
{
    ActiveTabLabel.Text = TabContainer1.ActiveTab.ID;
}
  protected void ExpertList_DataBound(object sender, EventArgs)
{
    ExpertList_SelectedIndexChanged(ExpertList, EventArgs.Empty);
    TabContainer1_ActiveTabChanged(ExpertList, EventArgs.Empty);
}
```

Code file [TabContainerSample.aspx] available for download at Wrox.

The ExpertList_SelectedIndexChanged event handler splits the SelectValue string that contains the expert data (such as Expertise, Description, and Photo) by separated signs, and sets the appropriate label and image controls with these values. Note that the controls within Tabs cannot be accessed directly, unless you do have members within the class representing the page. You can address them with the Page.FindControl method. For example, the control with the identifier Photo within the PhotoPanel can be accessed by the address TabContainer1$Photo.

The TabContainer1_ActiveTabChanged event handler displays the index of the selected tab. The ExpertList control is a data-bound control. As soon as the control is read and set up, the ExpertList_DataBound method is called, and the information within the TabContainer is refreshed.

Although Listing 20-10 does not show it, the TabContainer and the label displaying the active tab is wrapped with an UpdatePanel, so all event happens asynchronously.

The TabContainer contains several interesting properties summarized in Table 20-3.

# Table 20-3: TabContainer Properties

| PROPERTY | DESCRIPTION |
| --- | --- |
| ActiveTabChanged | This event is fired on the server side when a tab is changed after a postback. |
| OnClientActiveTabChanged | The name of a JavaScript function to attach to the client-side tabChanged. |
| CssClass | A CSS class override used to define a custom look and feel for the tabs. |
| ActiveTabIndex | The index of the TabPanel to show. |
| Height | Sets the height of the tabs (does not include the TabPanel headers). |