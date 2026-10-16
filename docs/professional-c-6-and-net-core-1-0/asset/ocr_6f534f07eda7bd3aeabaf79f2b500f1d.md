cases where street view is supported by the device, you can try to find nearby street-side places using the static method FindNearbyAsync of the StreetsidePanorama class. Street-side experience is available only for some locations. You can test to find out whether it is available in your location. If StreetsidePanorama information is available, it can be passed to the StreetsideExperience constructor and assigned to the CustomExperience property of the MapControl (code file MapSample/ViewModels/MapsViewModel.cs):

```
public async void StartStreetViewAsync()
{
    if (_mapControl.IsStreetsideSupported)
    {
        var panorama = await
StreetsidePanorama.FindNearbyAsync(CurrentPosition);
        if (panorama == null)
        {
            var dlg = new MessageDialog("No streetside available here");
            await dlg.ShowAsync();
            return;
        }
        IsStreetView = true;
        _mapControl.CustomExperience = new
StreetsideExperience(panorama);
    }
}
```

Street-side experience looks like what’s shown in Figure 33.15.