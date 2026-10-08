```
ExpandedText='Hide Details...'
CollapsedText='(Show Details...)'
ExpandedImage='/Images/HideDetails.png'
CollapsedImage='/Images/ShowDetails.png'
SuppressPostBack='true' />
<asp:DropShadowExtender ID="DropShadowExtender1" runat="server"
TargetControlID="CSharpSharpPanel"
Width="80"
Rounded="true"
Radius="6"
Opacity=".25"
TrackPosition="true" />
<hr />
<hr />
<div style="height:300px; width:250px; float: left; padding: 5px;">
<asp:Panel ID="HandlePanel" runat="server" Width="100%" Height="20px"
Style="z-index:20px;"\BorderStyle="Solid" BorderWidth="1px" BorderColor="black">
<div style="cursor:move">Drag me</div>
<asp:Panel ID="InfoPanel" runat="server" Width="100%" Height="20px"
Style="overflow:auto; padding: 8px; Background=#F4BCC"
BorderWidth="2px" BorderColor="black"
BorderStyle="Solid">
<div>
<p>
The version of COM provides dynamic binding as a unified
approach to selecting and carrying out operations dynamically.
Operations can be uniformly applied on various objects
independently of whether a specific object comes from COM
(through interoperability), IronRuby, IronPython, the HTML
DOM, or from any other dynamic context.
</p>
</div>
</asp:Panel>
</div>
<div style="clear: both;"></div>
<asp:DraggableExtender ID="DraggableExtender1" runat="server"
TargetControlID="DraggablePanel"
DragHandleID="HandlePanel" />
</div>
</form>
<body>
</html>
```

Code file [PanelExtendersSample.aspx] available for download at Wrox.com

You can set controls to expand and collapse the panel through the ExpandControlID and CollapsiblePanel properties, respectively. You can also specify the style and images for the panel with the ExpandedText, CollapsedText, ExpandedImage, and CollapsedImage properties. When you set the SuppressPostBack property to True, no postbacks are initiated when you expand or collapse the panel.