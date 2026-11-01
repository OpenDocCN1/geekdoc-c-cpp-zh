```
<TextBlock x:Name="textBlockCurrentImageDisplayName"
Margins="10,10,10,0" FontSize="24" FontWeight="Bold"
RelativePanel.AlignLeftWithPanel="True"
RelativePanel.AlignRightWithPanel="True" />
<TextBlock x:Name="textBlockCurrentImageHeight" Margin="10,10,10,0"
FontSize="24" FontWeight="Bold"
RelativePanel.AlignLeftWithPanel="True"
RelativePanel.AlignRightWithPanel="True"
RelativePanel.Below="textBlockCurrentImageDisplayName" />
<TextBlock x:Name="textBlockCurrentImageWidth" Margin="10,10,10,0"
FontSize="24" FontWeight="Bold"
RelativePanel.AlignLeftWithPanel="True"
RelativePanel.AlignRightWithPanel="True"
RelativePanel.Below="textBlockCurrentImageHeight" />
```

5. Add the following Visual State Manager to control the appearance when the app is resizing. Add it as the first child to the Grid tag:

```
<VisualStateManager.VisualStateGroups>
    <VisualStateGroup>
        <VisualState x:Name="narrowView">
            <VisualState.StateTriggers>
                <AdaptiveTrigger MinWindowWidth="0" />
            </VisualState.StateTriggers>
            <VisualState.Setters>
                <Setter Target="RightPanel.(RelativePanel.Below)" Value="LeftPanel" />
                <Setter Target="RightPanel.(RelativePanel.AlignLeftWithPanel)" Value="True" />
                <Setter Target="RightPanel.(RelativePanel.AlignRightWithPanel)" Value="True" />
                <Setter Target="RightPanel.Margin" Value="0,10,0,0" />
                <Setter Target="LeftPanel.(RelativePanel.AlignTopWithPanel)" Value="True" />
                <Setter Target="LeftPanel.(RelativePanel.AlignLeftWithPanel)" Value="True" />
                <Setter Target="LeftPanel.(RelativePanel.AlignRightWithPanel)" Value="True" />
                <Setter Target="LeftPanel.Height" Value="560" />
            </VisualState.Setters>
        </VisualState>
        <VisualState x:Name="wideView">
            <VisualState.StateTriggers>
                <AdaptiveTrigger MinWindowWidth="720" />
            </VisualState.StateTriggers>
            <VisualState.Setters>
                <Setter Target="RightPanel.(RelativePanel.AlignBottomWithPanel)" Value="True" />
                <Setter Target="RightPanel.(RelativePanel.AlignRightWithPanel)" Value="True" />
                <Setter Target="RightPanel.(RelativePanel.AlignTopWithPanel)" Value="True" />
                <Setter Target="RightPanel.Width" Value="200" />
                <Setter Target="LeftPanel.(RelativePanel.LeftOf)" Value="RightPanel" />
                <Setter Target="LeftPanel.(RelativePanel.AlignBottomWithPanel)" Value="True" />
            </VisualState.Setters>
        </VisualState>
    </VisualStateGroup>
</VisualStateManager.VisualStateGroups>
```