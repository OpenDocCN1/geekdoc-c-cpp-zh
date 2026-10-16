
```
var picker = new FileSavePicker();
picker.SuggestedStartLocation =
PickerLocationId.VideosLibrary;
picker.FileTypeChoices.Add("Video File", new string[]
{".wmv" });
    StorageFile fileDestination = await
picker.PickSaveFileAsync();
    if (fileDestination != null)
    {
        await file.CopyAndReplaceAsync(fileDestination);
    }
}
```

In cases where the user should be offered the option to capture either a video or a photo, you can pass the parameter CameraCaptureUIMode.PhotoOrVideo to the method CaptureFileAsync.

Because the camera also records location information, when the user runs the app for the first time, he or she is asked if recording location information should be allowed (see Figure 33.9).

![](img/3d365b72b289213a91ade7eb366b8f35_1271_0.png)

Figure 33.9

Running the application, you can record photos and videos.

## Geolocation and MapControl

Knowing the location of the user is an important aspect of apps, whether it’s an app to show a map, an app that shows the weather of the area of the user, or an app for which you need to decide in what nearest cloud center the data of the user should be saved. When ads are used in the app, the user location can be important to show ads from the near area (if available).

With UWP apps you can also show maps. With Windows 10, a MapControl is available as part of the Windows API, and you don’t need to use additional libraries, such as the Bing SDK, for doing this.

The sample app uses both the Geolocator (namespace Windows.Devices.Geolocation), to give information about the address of the user, and the MapControl (namespace Windows.UI.Xaml.Controls.Maps). Of course, you can also use these types independent of each other in your apps.

### Using the MapControl

With the sample app, a MapControl is defined in the MainPage where different properties and events bind to values from the MapsViewModel that is accessed via the ViewModel property of the page. This way, you can dynamically change some settings in the app and see different features available with the MapControl (code file MapSample/MainPage.xaml):

```
<maps:MapControl x:Name="map"
    Center="{x:Bind ViewModel.CurrentPosition, Mode=OneWay}"
    MapTapped="{x:Bind ViewModel.OnMapTapped, Mode=OneTime}"
    Style="{x:Bind ViewModel.CurrentMapStyle, Mode=OneWay}"
    ZoomLevel="{x:Bind Path=ViewModel.ZoomLevel, Mode=OneWay}"
    DesiredPitch="{x:Bind Path=ViewModel.DesiredPitch,
Mode=OneWay}"
    TrafficFlowVisible="{x:Bind checkTrafficFlow.IsChecked,
Mode=OneWay,
    Converter={StaticResource nbtob}}"
    BusinessLandmarksVisible="{x:Bind checkBusinessLandmarks.IsChecked,
    Mode=OneWay, Converter={StaticResource nbtob}}"
    LandmarksVisible="{x:Bind checkLandmarks.IsChecked,
Mode=OneWay,
    Converter={StaticResource nbtob}}"
    PedestrianFeaturesVisible="{x:Bind checkPedestrianFeatures.IsChecked,
    Mode=OneWay, Converter={StaticResource nbtob}}" />
```

The sample app defines controls to configure the MapControl within the Pane of the SplitView that is positioned on the right side. The MapControl is defined within the content of the SplitView. You can read more about the SplitView control in Chapter 32.

With the code-behind file, the ViewModel property is defined, and a MapsViewModel is instantiated by passing the MapControl to the constructor. Usually it’s best to avoid having Windows controls directly accessible to the view model, and you should only use data binding to map. However, when you use some special features, such as street-side experience, it’s easier to directly use the MapControl in the MapsViewModel class. Because this view model type is not doing anything else and cannot be used on anything other than Windows devices anyway, it’s a compromise for passing the MapControl to the constructor of the MapsViewModel (code file MapSample/MainPage.xaml.cs):

```
public sealed partial class MainPage: Page
{
    public MainPage()
    {
        this.InitializeComponent();
        ViewModel = new MapsViewModel(map);
    }

    public MapsViewModel ViewModel { get; }
}
```

The constructor of the MapsViewModel initializes some properties that are bound to properties of the MapControl, such as the position of the map to a location within Vienna, the map style to a road variant, the pitch level to 0, and the zoom level to 12 (code file MapSample/ViewModels/MapsViewModel.cs):

```
public class MapsViewModel: BindableBase
{
	private readonly CoreDispatcher _dispatcher;
	private readonly Geolocator _locator = new Geolocator();
	private readonly MapControl _mapControl;

	public MapsViewModel(MapControl mapControl)
	{
		_mapControl = mapControl;
		StopStreetViewCommand = new DelegateCommand(
			StopStreetView, () => IsStreetView);
		StartStreetViewCommand = new DelegateCommand(
			StartStreetViewAsync, () => !IsStreetView);
		if (!DesignMode.DesignModeEnabled)
		{
			_dispatcher = CoreWindow.GetForCurrentThread().Dispatcher;
		}
		_locator.StatusChanged += async (s, e) =>
		{
			await _dispatcher.RunAsync(CoreDispatcherPriority.Low, () =>
				PositionStatus = e.Status);
		};
		// initialize defaults at startup
		CurrentPosition = new Geopoint(
			new BasicGeoposition { Latitude = 48.2, Longitude = 16.3
			});
		CurrentMapStyle = MapStyle.Road;
		DesiredPitch = 0;
		ZoomLevel = 12;
	}
```

Upon starting the app with the initial configuration, you can see the maps loaded with a location in Vienna as defined by the BasicGeoposition, the controls on the right side for managing the MapControl, and textual information about the loading status of the map (see Figure 33.10).

![](img/3d365b72b289213a91ade7eb366b8f35_1274_0.png)

Figure 33.10

When you zoom in, change the pitch level, and select landmarks and business landmarks to be visible, you can see famous buildings such as the Stephansdom in Vienna, as shown in Figure 33.11.

![](img/3d365b72b289213a91ade7eb366b8f35_1275_0.png)

Figure 33.11

When you switch to the Aerial view, you can see real images, as shown in Figure 33.12.

Figure 33.12

Some locations also show nice images with the Aerial3D view, as shown in Figure 33.13.

![](img/3d365b72b289213a91ade7eb366b8f35_1277_0.png)

Figure 33.13

### Location Information with Geolocator

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

The `Geoposition` instance returned from `GetGeopositionAsync` lists information about how the `Geolocator` came to the conclusion of the position: using a cellular network with a phone, satellite, a Wi-Fi network that is recorded, or an IP address. When you configure the `Geolocator`, you can specify how accurate the information should be. By setting the property `DesiredAccuracyInMeters`, you can define how exact the location should be within a meter range. Of course, this accuracy is what you hope for, but it might not be possible to achieve. If the location should be more exact, GPS information from accessing satellite information can be used. Depending on the technology needed, more battery is used, so you shouldn’t specify such accuracy if it’s not really necessary. Satellite or cellular information cannot be used if the device doesn’t offer these features. In those cases, you can use only the Wi-Fi network (if available) or an IP address. Of course, the IP address can be imprecise. Maybe you’re getting the geolocation of an IP provider instead of the user. With the device and network I’m using, I get an accuracy of 64 meters. The source of the position is Wi-Fi. The result is very accurate. You can see the map in Figure 33.14.

![](img/3d365b72b289213a91ade7eb366b8f35_1278_0.png)

Figure 33.14

### Street-Side Experience

Another feature offered by the `MapControl` is street-side experience. This feature is not available with all devices. You need to check the `IsStreetsideSupported` property from the `MapControl` before using it. In
