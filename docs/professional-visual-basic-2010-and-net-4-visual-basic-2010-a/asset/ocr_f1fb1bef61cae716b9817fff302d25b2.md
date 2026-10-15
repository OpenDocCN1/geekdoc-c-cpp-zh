```
Public Property Details As List(Of OrderDetail)

Public Sub New()
    Details = New List(Of OrderDetail)
End Sub
End Class
```

Code snippet from OrderManager

The OrderDetail class is an individual line item within an order. Again, for this example it is greatly simplified:

```
Public Class OrderDetail
    Public Property Parent As Order
    Public Property ItemName As String
    Public Property Quantity As Integer
End Class
```

Code snippet from OrderManager

The OrderSystem class is a general manager class for the orders. In addition to the functionality for this demo, it would likely be responsible for saving orders to a database, and so on:

```
Public Class OrderSystem

    Public Function GetOrderFromDropFile(ByVal path As String) As Order
        Dim result As Order = Nothing
        Dim files As String()
        Dim doc As New XDocument
        Dim detail As OrderDetail

        files = IO.Directory.GetFiles(path)
        If files.Length > 0 Then
            doc = XDocument.Load(files(0))
            'load header
            result = New Order
            With result
                .OrderID = CInt(doc.Root.Attribute("id").Value)
                .CustomerName = doc.Root.Element("customerName").Value
                .OrderDate = CDate(doc.Root.Element("orderDate").Value)
                .ShipAddress = doc.Root.Element("shipAddress").Value
            End With
            'load detail rows
            Dim details As List(Of XElement) = (From item In doc.Descendants
                                                Where item.Name = "orderDetail"
                                                Select item).ToList

            For Each d In details
                detail = New OrderDetail
                With detail
                    .Parent = result
                    .ItemName = d.Element("itemName").Value
                    .Quantity = CDec(d.Element("quantity").Value)
                End With
                result.Details.Add(detail)
            Next
            'delete file to avoid calling this again
            'likely you would move to a backup directory instead
            '
            IO.File.Delete(files(0))
        End If

        Return result
```