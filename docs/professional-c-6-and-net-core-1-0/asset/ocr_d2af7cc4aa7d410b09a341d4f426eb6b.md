> **NOTE** *Here are some examples of features that users had trouble finding from Microsoft’s own products. The Xbox was the first device to offer a user interface with large tiles. The search feature was available directly below the tiles. Although this button was available directly in front of the user, users didn’t see it. Microsoft moved the search functionality within a tile, and now users are able to find it. Another example is the physical search button on the Windows Phone. This button was meant to be used to search within apps. Users complained about not having an option to search within email because they didn’t think to press this physical button to search for emails. Microsoft changed the functionality. Now the physical search button is used only to search content from the web, and the mail app has its own Search button. Windows 8 had a similar issue with search; users didn’t use the search functionality from the charms bar to search within apps. Windows 8.1 changed the guideline to use search from the charms bar, and now the app contains its own search box; in Windows 10 there’s also an auto suggest box. Does it look like some communalities?*

# Creating a Universal Windows App

One of the sample apps for making use of Application Insights is a Universal Windows Platform app with two pages—`MainPage` and `SecondPage`—and just a few button and textbox controls to simulate an action, throw an exception, and navigate between pages. The user interface is defined in the following code snippet (code file `WinAppInsights/MainPage.xaml`):

```
```xml
<StackPanel Orientation="Vertical">
    <Button Content="Navigate to SecondPage" Click="OnNavigateToSecondPage" />
    <TextBox x:Name="SampleDataText" Header="Sample Data" />
    <Button Content="Action" Click="OnAction" />
    <Button Content="Create Error" Click="OnError" />
</StackPanel>
```
```

Clicking on the Navigate to SecondPage button invokes the `OnNavigateToSecondPage` event handler method and navigates to the second page (code file `WinAppInsights/MainPage.xaml.cs`):

```
```csharp
private void OnNavigateToSecondPage(object sender,
    RoutedEventArgs e)
{
    this.Frame.Navigate(typeof(SecondPage));
}
```
```

With the `OnAction` method, a dialog shows the data entered by the user:

```
```csharp
private async void OnAction(object sender, RoutedEventArgs e)
{
    var dialog = new ContentDialog
    {
        Title = "Sample",
```
```