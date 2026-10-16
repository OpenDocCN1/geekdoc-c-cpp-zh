The BoolToNullableBoolConverter is instantiated with the resources of the page (code file AppShellSample/AppShell.xaml):

```
<Page.Resources>
    <conv:BoolToNullableBoolConverter x:Key="boolConverter" />
</Page.Resources>
```

With the ToggleButton, the IsChecked property is bound to the IsPaneOpen of the split view, using the BoolToNullableBoolConverter referenced as a static resource.

```
<ToggleButton x:Name="TogglePaneButton"
              TabIndex="1"
              Style="{StaticResource SplitViewTogglePaneButtonStyle}"
              IsChecked="{x:Bind Path=RootSplitView.IsPaneOpen, Mode=TwoWay, Converter={StaticResource boolConverter}}"
              Unchecked="HamburgerMenu_UnChecked"
              AutomationProperties.Name="Menu"
              ToolTipService.ToolTip="Menu" />
```

> NOTE Compiled binding doesn’t support element-to-element binding as traditional binding does. However, as the SplitView has the name RootSplitView assigned, this variable can be directly used from code, and thus from compiled binding.

Lastly, some content needs to be added to the SplitView pane.

# Adding Content to the SplitView Pane

The pane of the SplitView should now list menu buttons for navigation to different pages. The sample code makes use of simple button controls within a ListView control. The ListView defines a Header, Footer, and Items section. The Header section includes a back button. Previously, the system back button was used with the help of the SystemNavigationManager. Instead of this system back button, you can use a custom button, as is used here. This button element binds the IsEnabled property to AppFrame.CanGoBack to change the IsEnabled mode depending on whether there’s a back stack available. The Footer of the ListView defines a settings button. Within the items list of the ListView, Home and Edit buttons are created to navigate to these corresponding pages (code file AppShellSample/AppShell.xaml):

```
<SplitView.Pane>
    <ListView TabIndex="3" x:Name="NavMenuList" Margin="0,48,0,0">
        <ListView.Header>
            <Button x:Name="BackButton"
                    TabIndex="2"
                    Style="{StaticResource NavigationBackButtonStyle}"
                    IsEnabled="{x:Bind AppFrame.CanGoBack, Mode=OneWay}"
                    Width="{x:Bind Path=NavMenuList.Width, Mode=OneWay}"
                    HorizontalAlignment="
                        "{x:Bind Path=NavMenuList.HorizontalAlignment,
```