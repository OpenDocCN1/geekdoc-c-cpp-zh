```
Parallel.For(0, 1000, doLoopWork);
...
private void doLoopWork(int i, ParallelLoopState p)
{
    if (i > 600)
    {
        p.Stop();
    }
}
```

# To display the status of each task

+   1. In Visual Studio, display the MainPage.xaml file in the Design View window.
2. In the XAML pane, add the following markup to the definition of the MainPage form before the final closing </Grid> tag, as shown in bold in the following code:

Click here to view code image

```
<Image x:Name="graphImage" Grid.Column="1" Stretch="Fill" />
</Grid>
<TextBlock x:Name="messages" Grid.Row="4" FontSize="18" HorizontalAlignment="Left"/>
</Page>
```

This markup adds a TextBlock control named messages to the bottom of the form.

+   3. Display the MainPage.xaml.cs file in the Code and Text Editor window and find the plotButton_Click method.
4. Add the code shown in bold to build this method. These statements generate a string that contains the status of each task after it has finished running and display this string in the messages TextBlock control at the bottom of the form.

Click here to view code image

```
private async void plotButton_Click(object sender, RoutedEventArgs e)
{
```