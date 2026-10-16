![](bbox=[0.105, 0.064, 0.894, 0.475])

# Figure 33.13

# Location Information with Geolocator

Next, you need to get the actual position of the user with the help of the Geolocator instance _locator. The method GetPositionAsync returns the geolocation by returning a Geoposition instance. The result is applied to the CurrentPosition property of the view model that is bound to the center of the MapControl (code file MapSample/ViewModels/MapsViewModel.cs):

```
public async void GetCurrentPositionAsync()
{
    try
    {
        Geoposition position = await _locator.GetGeopositionAsync(
            TimeSpan.FromMinutes(5), TimeSpan.FromSeconds(5));
        CurrentPosition = new Geopoint(new BasicGeoposition
        {
            Longitude = position.Coordinate.Point.Position.Longitude,
            Latitude = position.Coordinate.Point.Position.Latitude
        });
    }
    catch (UnauthorizedAccessException ex)
    {
        await new MessageDialog(ex.Message).ShowAsync();
    }
}
```