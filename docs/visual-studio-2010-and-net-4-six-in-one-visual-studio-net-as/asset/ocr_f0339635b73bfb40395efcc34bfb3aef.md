# LISTING 16-9: BinaryStreamRendering.aspx

![](bbox=[0.045, 0.133, 0.098, 0.175])

```
<%@ Page Language="C#" AutoEventWireup="true"
CodeBehind="BinaryStreamRendering.aspx.cs"
Inherits="PetShopCharts.BinaryStreamRendering">

<!DOCTYPE type html HTML 1.0 Transitional//EN//
"http://www.w3.org/TR/html1/DTD-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <meta charset="server">
  <title>Sales Data through binary stream rendering</title>
</head>
<body>
  <form id="form1" runat="server">
  <table>
    <tr>
      <td>
        <h2>Dog Sales in the Western Region</h2>
        <asp:Image Id="ImageWest"
               ImageUrl="DogSalesChart.aspx?region=West"
               runat="server" Height="500px" Width="800px" />
      </td>
    </tr>
    <tr>
      <td>
        <h4 id="h4">Dog Sales in the Eastern Region</h4>
        <asp:Image Id="ImageEast"
               ImageUrl="DogSalesChart.aspx?region=East"
               runat="server" Height="250px" Width="400px" />
      </td>
    </tr>
    <tr>
      <td>
        <h4 id="h4">Dog Sales in the Northern Region</h4>
        <asp:Image Id="ImageNorth"
               ImageUrl="DogSalesChart.aspx?region=North"
               runat="server" Height="250px" Width="400px" />
      </td>
    </tr>
  </table>
  </form>
</body>
</html>
```

> Code file [BinaryStreamRendering.aspx] available for download at Wrox.com

This file contains three <asp:Image> elements referencing DogSalesChart.aspx, with three different region settings. Of course, you can set any other parameters of the Image element. The second and third images display the original image in half size. Figure 16-9 shows a part of the BinaryStreamRendering.aspx page as you see it in the browser.