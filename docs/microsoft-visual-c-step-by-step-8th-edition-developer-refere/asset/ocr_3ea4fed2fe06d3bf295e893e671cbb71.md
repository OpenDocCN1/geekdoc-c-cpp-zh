| Control | Property | Value |
|---|---|---|
| First TextBox | x:Name | id |
|  | HorizontalAlignment | Left |
|  | Margin | 300,240,0,0 |
|  | TextWrapping | Wrap |
|  | Text |  |
|  | VerticalAlignment | Top |
|  | FontSize | 20 |
|  | IsReadOnly | True |
| Second TextBox | x:Name | firstName |
|  | HorizontalAlignment | Left |
|  | Margin | 550,240,0,0 |
|  | TextWrapping | Wrap |
|  | Text |  |
|  | VerticalAlignment | Top |
|  | FontSize | 20 |
| Third TextBox | x:Name | lastName |
|  | HorizontalAlignment | Left |
|  | Margin | 875,240,0,0 |
|  | TextWrapping | Wrap |
|  | Text |  |
|  | VerticalAlignment | Top |
|  | FontSize | 20 |

The following code shows the equivalent XAML markup for these controls:

Click here to view code image

```
<TextBox x:Name="id" HorizontalAlignment="Left"
Margin="300,240,0,0" TextWrapping="Wrap"
Text="" VerticalAlignment="Top" FontSize="20" IsReadOnly="True"/>
<TextBox x:Name="firstName" HorizontalAlignment="Left"
Margin="550,240,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="300"
FontSize="20"/>
<TextBox x:Name="lastName" HorizontalAlignment="Left"
Margin="875,240,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="300"
FontSize="20"/>
```