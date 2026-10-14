```
<Page
    x:Class="Customers.MainPage"
    ...>

    <Grid Style="{StaticResource GridStyle}">
        ...
        <Grid x:Name="customersTabularView" ...>
            ...
            <Grid Grid.Row="2">
                ...
                <TextBlock Grid.Row="6" Grid.Column="1" Grid.ColumnSpan="7" Style="{StaticResource ErrorMessageStyle}"/>
                </Grid>
            </Grid>
            <Grid x:Name="customersColumnarView" Margin="20,10,20,110" ...>
                ...
                <Grid Grid.Row="1">
                    ...
                    <TextBlock Grid.Row="6" Grid.Column="0" Grid.ColumnSpan="2" Style="{StaticResource ErrorMessageStyle}"/>
                    </Grid>
                </Grid>
            ...
        </Grid>
    ...
</Page>
```