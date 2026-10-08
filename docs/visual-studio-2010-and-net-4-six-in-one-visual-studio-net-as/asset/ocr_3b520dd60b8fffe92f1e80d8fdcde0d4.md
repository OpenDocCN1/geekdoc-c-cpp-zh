# LISTING 16-8: DogSalChart.aspx

![](bbox=[0.104, 0.117, 0.148, 0.153])

```
<@ Page Language="C#" AutoEventWire="true" CodeBehind="DogSalChart.aspx.cs"
Inherits="PetShopCharts.DogSalChartData" %>
<asp:chart id="Chart1" server="server" height="500" width="800"
rendertype="BinaryStreaming" BackColor="Khaki" BackGradientStyle="DiagonalLeft"
BackSecondaryColor="DarkKoldenrod">
<asp:ChartArea>
<asp:Axis TitleName="Sales" Number="True" Font="Calibri, 14.25pt, style=bold"
MinimumGrid="True" Interval="100" LineColor="Silver" />
</asp:Axis>
<asp:AxisX Interval="*1" IsLabelFit="False" LabelAutoFitFontSize="12"
LabelAutoFitFontSize="12"
<asp:MajorGrid LineColor="Silver" />
<asp:LabelStyle Font="Calibri, 12pt, style=bold" />
</asp:AxisX>
</asp:ChartArea>
</asp:chart>
<asp:Legend>
<asp:Legend BackColor="Papawhip" BorderColor="DimGray"
DockedToChartArea="ChartArea" Name="Legend1"/>
</asp:Legend>
</asp:chart>
```

Code file [DogSalChart.aspx] available for download at Wrox.com.

As you see, this chart does not contain any HTML elements, only the <asp:chart> element.
Fortunately, the designer still supports all the chart properties just as it were embedded in a usual .aspx page. The RenderType of the chart is set to BinaryStreaming.
The DogSalChart.aspx contains the logic that operates chart with the DataBindCrossTable methods using the same pattern as shown in Listing 16-6. The region parameter to query the sales queries for the specified region, by the following code extracts

```
protected void Page_Load(object sender, EventArgs e)
{
    var region = Request["region"];
    var connection = Helpers.Utility.GetDataConnection(this);
    var commandStr = "SELECT Name, Total, ShopName from DogSalChart data where " +
    " Region = '" + region + '\';";
    var command = new OleDbCommand(commandStr, connection);
    //
```

Listing 16-9 shows the BinaryStreamingRendering.aspx file that references DogSalChart.aspx.