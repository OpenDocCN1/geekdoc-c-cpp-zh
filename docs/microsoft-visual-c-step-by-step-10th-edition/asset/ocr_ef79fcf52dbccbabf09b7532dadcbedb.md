```
<VisualStateManager.VisualStateGroups>
  <VisualStateGroup>
    <VisualState x:Name="TabularLayout">
      <VisualState.StateTriggers>
        <AdaptiveTrigger MinWidth="660"/>
      </VisualState.StateTriggers>
      <VisualState.Setters>
        <Setter Target="customersTabularView.Visibility" Value="Visible"/>
        <Setter Target="customersColumnarView.Visibility" Value="Collapsed"/>
      </VisualState.Setters>
    </VisualState>
  </VisualStateGroup>
</VisualStateManager.VisualStateGroups>
```