DataBoundComboBox is not. The two ComboBox instances raise a few events that let you examine how they work. By both of them respond to the SelectedChanged event, and display the current selection. Listing 20-9 shows the code behind the UI.

# LISTING 20-9: ComboBoxSample.ascx

```
using System;
using System.Data;
using System.Data.OleDb;
using System.Web.UI.WebControls;
using AjaxControlToolkit;

namespace ActControlSamples
{
public partial class ComboBoxSample : System.Web.UI.Page{
    protected void Page_Load(object sender, EventArgs e)
    }

    protected void AutoCompleteList_SelectedIndexChanged(object sender, EventArgs e)
    {
        var autoComplete = (ComboBoxAutoCompleteMode)Enum.Parse(
typeof(ComboBox.AutoCompleteMode),
AutoCompleteList.SelectedValue);
        SimpleComboBox.Auto.AutoCompleteMode = autoComplete;
        DataBoundComboBox.Auto.AutoCompleteMode = autoComplete;
    }

    protected void SimpleLabel_SelectedIndexChanged(object sender, EventArgs e)
    {
        SimpleLabel.Text = String.Format("{0}: {1}",
SimpleComboBox.SelectedValue, SimpleComboBox.SelectedItem);
    }

    protected void ComboBoxItem_ItemInserted(object sender, EventArgs e)
    {
        SimpleLabel.Text = String.Format("{0}: {1}",
SimpleComboBox.SelectedValue, SimpleComboBox.SelectedItem);
    }

    protected void SimpleComboBox_ItemInserting(object sender,
ComboBoxItemInsertEventArgs e)
    {
        if (e.Item.Text.StartsWith("Q"))
        {
            e.Cancel = true;
            return;
        }
}
```