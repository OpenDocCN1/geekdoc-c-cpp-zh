
```
private async void OnRequestReceived(AppServiceConnection sender,
    AppServiceRequestReceivedEventArgs args)
{
    AppServiceDeferral deferral = args.GetDeferral();
    try
    {
        ValueSet message = args.Request.Message;
        ValueSet result = null;

        switch (message["command"].ToString())
        {
            case"GET":
                result = GetBooks();
                break;
            case"POST":
                result = AddBook(message["book"].ToString());
                break;
            default:
                break;
        }
        await args.Request.SendResponseAsync(result);
    }
    finally
    {
        deferral.Complete();
    }
}
```

The GetBooks method uses the BooksRepository to get all the books in JSON format, and it creates a ValueSet with the result key:

```
private ValueSet GetBooks()
{
    var result = new ValueSet();
    result.Add("result",
BooksRepository.Instance.Books.ToJson());
    return result;
}
```

The AddBook method uses the repository to add a book, and returns a ValueSet with a result key and the value ok:

```
private ValueSet AddBook(string book)
{
    BooksRepository.Instance.AddBook(book.ToBook());
    var result = new ValueSet();
    result.Add("result","ok");
    return result;
}
```

## Registering the App Service

You now need to register the app service with the operating system. This is done by creating a normal UWP app that has a reference to the BooksCacheService. With this app, you must define a declaration in the package.appxmanifest (see Figure 33.8). Add an app service to the app declaration list and give it a name. You need to set the entry point to the background task, including the namespace and the class name.

![](img/3d365b72b289213a91ade7eb366b8f35_1267_0.png)

### Figure 33.8

For the client app, you need the name of the app that you defined with the package.appxmanifest as well as the package name. To see the package name, you can invoke Package.Current.Id.FamilyName. To see this name easily, it is written to the property PackageFamilyName that is bound within a control in the user interface (code file AppServices/BooksCacheProvider/MainPage.xaml.cs):

```
public sealed partial class MainPage: Page
{
    public MainPage()
    {
        this.InitializeComponent();
        PackageFamilyName = Package.Current.Id.FamilyName;
    }

    public string PackageFamilyName
    {
        get { return (string)GetValue(PackageFamilyNameProperty); }
        set { SetValue(PackageFamilyNameProperty, value); }
    }

    public static readonly DependencyProperty
PackageFamilyNameProperty =
        DependencyProperty.Register("PackageFamilyName",
typeof(string),
            typeof(MainPage), new PropertyMetadata(string.Empty));
}
```

When you run this app, it registers the background task and shows the package name that you need for the client app.

## Calling the App Service

With the client app, the app service can now be called. The main parts of the client app BooksCacheClient are implemented with the view model. The Books property is bound in the UI to show all books returned from the service. This collection is filled by the GetBooksAsync

method. GetBooksAsync creates a ValueSet with the GET command that is sent to the app service with the helper method SendMessageAsync. This helper method returns a JSON string, which in turn is converted to a Book collection that is used to fill the ObservableCollection for the Books property (code file AppServices/BooksCacheClient/ViewModels/BooksViewModel.cs):

```
public class BooksViewModel
{
    private const string BookServiceName
="com.CNinnovation.BooksCache";
    private const string BooksPackageName =
        "CNinnovation.Samples.BookCache_p2wxv0ry6mv8g";

    public ObservableCollection<Book> Books { get; } =
        new ObservableCollection<Book>();

    public async void GetBooksAsync()
    {
        var message = new ValueSet();
        message.Add("command","GET");
        string json = await SendMessageAsync(message);
        IEnumerable<Book> books = json.ToBooks();
        foreach (var book in books)
        {
            Books.Add(book);
        }
    }
}
```

The method PostBookAsync creates a Book object, serializes it to JSON, and sends it via a ValueSet to the SendMessageAsync method:

```
public string NewBookTitle { get; set; }
    public string NewBookPublisher { get; set; }

    public async void PostBookAsync()
    {
        var message = new ValueSet();
        message.Add("command","POST");
        string json = new Book
        {
            Title = NewBookTitle,
            Publisher = NewBookPublisher
        }.ToJson();
        message.Add("book", json);
        string result = await SendMessageAsync(message);
    }
```

The app service–relevant client code is contained within the method SendMessageAsync. Here, an AppServiceConnection is created. The connection is closed after use by disposing it with the using statement. To map the connection to the correct service, the AppServiceName and PackageFamilyName properties need to be supplied. After setting these properties, the connection is opened by invoking the method OpenAsync. Only when the connection is opened successfully is a request sent with the ValueSet received from the calling method. The AppServiceConnection method SendMessageAsync makes the request to the service and returns an AppServiceResponse object. The response contains the result from the service, which is dealt with accordingly:

```
private async Task<string> SendMessageAsync(ValueSet message)
{
    using (var connection = new AppServiceConnection())
    {
        connection.AppServiceName = BookServiceName;
        connection.PackageFamilyName = BooksPackageName;

        AppServiceConnectionStatus status = await
connection.OpenAsync();
        if (status == AppServiceConnectionStatus.Success)
        {
            AppServiceResponse response =
                await connection.SendMessageAsync(message);
            if (response.Status == AppServiceResponseStatus.Success
&&
                response.Message.ContainsKey("result"))
            {
                string result = response.Message["result"].ToString();
                return result;
            }
            else
            {
                await ShowServiceErrorAsync(response.Status);
            }
        }
        else
        {
            await ShowConnectionErrorAsync(status);
        }
        return string.Empty;
    }
}
```

After building the solution and deploying both the provider and the client app, you can start the client app and invoke the service. You can also create multiple client apps calling the same service.

After communicating between apps, let’s make use of some hardware. The next section makes use of the camera to record photos and videos.

## Camera

As apps are becoming more and more visual, and more devices offer one or two cameras built-in, using the camera is becoming a more and more important aspect of apps—and it is easy to do with the Windows Runtime.

> NOTE Using the camera requires that you configure the Webcam capability in the Manifest Editor. For recording videos, you need to configure the Microphone capability as well.

Photos and videos can be captured with the CameraCaptureUI class (in the namespace Windows.Media.Capture). First, you need to configure the photo and video settings to use the CaptureFileAsync method. The first code snippet captures a photo. After instantiating the CameraCaptureUI class, PhotoSettings are applied. Possible photo

formats are JPG, JPGXR, and PNG. It is also possible to define cropping where the UI for the camera capture directly asks the user to select a clipping from the complete picture based on the cropping size. For cropping, you can define either a pixel size with the property CroppedSizeInPixels or just a ratio with CroppedAspectRatio. After the user takes the photo, the sample code uses the returned StorageFile from the method CaptureFileAsync to store it as a file inside a user-selected folder with the help of the FolderPicker (code file CameraSample/MainPage.xaml.cs)

```
private async void OnTakePhoto(object sender, RoutedEventArgs e)
{
    var cam = new CameraCaptureUI();
    cam.PhotoSettings.AllowCropping = true;
    cam.PhotoSettings.Format = CameraCaptureUIPhotoFormat.Png;
    cam.PhotoSettings.CroppedSizeInPixels = new Size(300, 300);
    StorageFile file = await
    cam.CaptureFileAsync(CameraCaptureUIMode.Photo);

    if (file != null)
    {
        var picker = new FileSavePicker();
        picker.SuggestedStartLocation =
        PickerLocationId.PicturesLibrary;
        picker.FileTypeChoices.Add("Image File", new string[]
        {".png"});
        StorageFile fileDestination = await
        picker.PickSaveFileAsync();
        if (fileDestination != null)
        {
            await file.CopyAndReplaceAsync(fileDestination);
        }
    }
}
```

The second code snippet is used to record a video. As before, you first need to take care of the configuration. Besides the PhotoSettings property, the CameraCaptureUI type defines the VideoSettings property. You can restrict the video recording based on the maximum resolution (using the enumeration value CameraCaptureUIMaxVideoResolution.HighestAvailable allows the user to select any available resolution) and the maximum duration. Possible video formats are WMV and MP4:

```
private async void OnRecordVideo(object sender, RoutedEventArgs e)
{
    var cam = new CameraCaptureUI();
    cam.VideoSettings.AllowTrimming = true;
    cam.VideoSettings.MaxResolution =
        CameraCaptureUIMaxVideoResolution.StandardDefinition;
    cam.VideoSettings.Format = CameraCaptureUIVideoFormat.Wmv;
    cam.VideoSettings.MaxDurationInSeconds = 5;
    StorageFile file = await cam.CaptureFileAsync(
        CameraCaptureUIMode.Video);

    if (file != null)
    {
```
