```
LoadingText="Loading..."
ServicePath=ExpertiseService.asmx ServiceMethod=GetDropDownContent /
<asp:CascadingDropDown Id="ccdExpert" runat="server" TargetControlID="ExpertList"
Category="Expert" ParentControlID="ExpertList"
PromptText="Please select an Expert"
LoadingText="Loading..." ServicePath=ExpertiseService.asmx
ServiceMethod=GetDropDownContent /
</form>
<body>
</html>
```

Code file [Default.aspx] available for download at Wix.com

The Triggers element within the UpdatePanel contains an AsyncPostBackTrigger attached to the ExpertList control. When the user selects an expert from the list, an asynchronous postback is sent to the server that can set the description and the photo of the expert. As soon as the asynchronous call completes, the controls within the update panel are refreshed with the description text and photo. Of course, you must write the code of the ExpertList_SelectedIndexChanged event handler, as shown in Listing 20-7.

![](bbox=[0.095, 0.447, 0.155, 0.483])

# LISTING 20-7: Default.aspx After Handling the ExpertList Events

```
using System;

namespace FindAnExpertDemo
{
    public partial class Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            if (!IsPostBack)
            {
                Photo.Visible = false;
            }
        }

        protected void ExpertList_SelectedIndexChanged(object sender, EventArgs e)
        {
            var fields = ExpertList.Value.Split('$');
            Description.Text = fields[2];
            Photo.ImageUrl = "/Photos/" + fields[1] + ".png";
            Photo.Visible = true;
        }
    }
}
```

Code file [Default.aspx.cs] available for download at Wix.com