![](bbox=[0.094, 0.088, 0.374, 0.449])

# FIGURE 26-16

Finally, the orders are simply displayed on the console to confirm they have been processed. This is done with another ForEach<T> activity that writes the order’s information, followed by each of the detail rows in the order (see Figure 26-16). The properties of these activities are defined as follows:

| ACTIVITY | PROPERTY | VALUE | DESCRIPTION |
|---|---|---|---|
| `ForEach<T>` | `TypeArgument` | `OrderManager.Order` | This will iterate over each of the orders in the collection to display them. |
|  | `Values` | `Orders` | This is a workflow variable containing the orders submitted. |
| `WriteLine` | `Text` | `String.Format("Order on {0} by {1} for:", item.OrderDate, item.CustomerName)` | Displays the contents of the order’s header information |
| `ForEach<T>` | `TypeArgument` | `OrderManager.OrderDetails` | This will iterate over the detail rows contained within the submitted order. |
|  | `Values` | `item.Details` | This is the collection of order details within the current order. |
| `WriteLine` | `Text` | `String.Format("{0} {1}(s)", detail.Quantity, detail.ItemName)` | Displays the contents of the fields of each order detail row |