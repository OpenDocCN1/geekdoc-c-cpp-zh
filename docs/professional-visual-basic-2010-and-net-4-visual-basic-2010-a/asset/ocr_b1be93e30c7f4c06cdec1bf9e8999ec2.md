```
TargetName="ContentFrame" Content="about"/>

</StackPanel>
<Border>

</Grid>

</Grid>

</UserControl>
```

Code snippet from MainPage.xaml

The code-behind file is as follows:

```
Imports System.Windows.Navigation

Partial Public Class MainPage
    Inherits UserControl

    Public Sub New()
        InitializeComponent()
    End Sub

    Private Sub ContentFrame_Navigated(ByVal sender As Object,
        ByVal e As NavigationEventArgs) Handles ContentFrame.Navigated
        For Each child As UIElement In LinksStackPanel.Children
            Dim hb As HyperlinkButton = TryCast(child, HyperlinkButton)
            If hb IsNot Nothing AndAlso hb.NavigateUri IsNot Nothing Then
                If hb.NavigateUri = e.Uri Then
                    VisualStateManager.GoToState(hb, "ActiveLink", True)
                Else
                    VisualStateManager.GoToState(hb, "InactiveLink", True)
                End If
            End If
        Next
    End Sub

    Private Sub ContentFrame_NavigationFailed(ByVal sender As Object,
    ByVal e As NavigationFailedEventArgs) Handles ContentFrame.NavigationFailed
        e.Handled = True
        Dim errorWindow As ChildWindow = New ErrorWindow(e.Uri)
        errorWindow.Show()
    End Sub
End Class
```

Code snippet from MainPage.xaml.vb

You probably noticed that this is very similar to what you learned about WPF. The general idea is the same. You can add controls to the XAML and then modify the code for the control. This separation of UI and code helps create a simple architecture for managing the application design. This separation is very useful when using both Visual Studio and Microsoft Expression Blend.

# CONTROLS

Just as in Windows forms development, Silverlight offers a large collection of controls that give you a lot of options for developing rich interfaces. In addition, you will find Silverlight development to be almost identical to WPF development, as both user interfaces use XAML as the layout method.