
```cpp
pImage->Construct();

Bitmap* pBitmap = new Bitmap();
pBitmap = pImage->DecodeN(String(L"/Res/image.jpg"),
BITMAP_PIXEL_FORMAT_RGB565);

pBitmap->Scale(Dimension(200, 120));

// In this example we use white as the masking colour. Any white
// pixels in the bitmap will be treated as transparent.
Color maskColour(Color::COLOR_WHITE);
pBitmap->SetMaskingColor(&maskColour);

// Draw bitmap on panel canvas
pCanvas->DrawBitmap(Point(140, 140), *pBitmap);

delete pCanvas;
delete pBitmap;
delete pImage;

return r;
```

This CameraOverlayPanel class can be used by the MainForm for creating the overlay panel for the camera preview image.

The Camera class provides several methods for controlling the camera device, some of which work asynchronously. So when the camera device is used in an application, the Osp::Media::ICameraEventListener listener must be implemented to receive events associated with the camera.

The following code snippet shows an example of the MainForm class definition:

```cpp
class MainForm :
    public Osp::UI::Controls::Form,
    public Osp::Media::ICameraEventListener
{
public:
    MainForm(void);
    ~MainForm(void);
    bool Initialize(void);

protected:
    Osp::Media::Camera* pCamera;

public:
    result OnInitializing(void);
    result OnTerminating(void);

    void OnCameraAutoFocused (bool completeCondition);
    void OnCameraCaptured (Osp::Base::ByteBuffer &capturedData,
        result r);
    void OnCameraErrorOccurred (Osp::Media::CameraErrorReason r);
    void OnCameraPreviewed (Osp::Base::ByteBuffer &previewedData,
        result r);
};
```

In this recipe only the preview functionality of the camera device is used and the display of the preview image is performed by the camera engine, so none of the ICameraEventListener methods need to be implemented.

The camera device and the overlay panel can be created during initialisation of the MainForm::OnInitializing().

- 1. Create an instance of the primary camera device and initialise it with the camera event listener.
- 2. Power on the camera.
- 3. Create an instance of the custom overlay panel CameraOverlayPanel.
- 4. Construct the panel to the required size using a Rectangle object.
- 5. Set the render rotation for the panel to portrait mode.
- 6. Add the panel to the MainForm.
- 7. Retrieve the information of the background buffer in which the camera preview image will be displayed.
- 8. Start displaying the preview image from the camera. In this example the camera device displays the preview image and the OnCameraPreviewed() listener callback is disabled.
- 9. Set the device screen to remain on and not be dimmed.

The following code snippet is an example of the MainForm's OnInitializing() method:

```cpp
result
MainForm::OnInitializing(void)
{
    result r = E_SUCCESS;

    // Create an instance of the primary Camera and register listener
    pCamera = new Camera();
    pCamera->Construct("this", CAMERA_PRIMARY);

    // Power on the camera
    pCamera->PowerOn();

    Osp::Graphics::BufferInfo buffer_info;

    // Create an instance of the CameraOverlayPanel and initialise
    CameraOverlayPanel* pCameraPanel = new CameraOverlayPanel();
    pCameraPanel->Initialize(Rectangle(0, 0, 480, 800));

    // Set the panel's renderer rotation - for portrait mode
    pCameraPanel->SetRendererRotation(OverlayPanel::ROTATION_90);

    // Add panel to MainForm
    AddControl(*pCameraPanel);

    // Get the information of the background buffer
    pCameraPanel->GetBackgroundBufferInfo(buffer_info);

    // Start displaying preview image from camera
    // Image will be drawn by camera object
    pCamera->StartPreview(&buffer_info, false);

    // Set the display to remain permanently on and not be dimmed
    Osp::System::PowerManager::KeepScreenOnState(true, false);

    return r;
}
```

When the application terminates, the camera device must be shut down correctly in the MainForm's OnTerminating() method:

- 1. Check the camera is powered on.
- 2. Stop displaying the preview image from the camera.
- 3. Power off the camera.

The following code snippet is an example of the MainForm's OnTerminating() method:

```cpp
result
MainForm::OnTerminating(void)
{
    result r = E_SUCCESS;

    // Check if camera is powered on
    if(pCamera->IsPoweredOn())
    {
        // Stop displaying the preview image and power off
        // the camera
        pCamera->StopPreview();
        pCamera->PowerOff();
    }

    delete pCamera;
    pCamera = null;

    return r;
}
```

## Hints, Pitfalls, and Related Topics

The CAMERA group privilege must be set in the application's manifest file in order to use the camera device.

The SYSTEM_SERVICE group privilege must be set in the application's manifest file in order to use the Power Manager functionality to keep the display permanently on and prevent it from dimming.

The IMAGE group privilege must be set in the application's manifest file in order to use the DecodeN() method from the Image class.

This recipe can also be tested in the simulator environment if there is a webcam connected to your computer. The camera control will display the preview from the webcam. In the current version of the SDK and firmware of the Wave device during writing of this recipe there is a slight discrepancy between the behaviour of the simulator and the Wave target device, which you should be aware of. By default, the CAMERA_PRIMARY on the target device is started in Landscape mode, so it is necessary to rotate the panel to Portrait mode. In the simulator environment, the camera starts in Portrait mode so the function call is not needed. See below:

```cpp
// Set the panel's renderer rotation - for portrait mode
pCameraPanel->SetRendererRotation(OverlayPanel::ROTATION_90);
```

If any controls such as buttons or labels need to be added to the custom overlay panel, they should be created and added in the CameraOverlayPanel::OnInitializing() method.

Setting the transparency colour of a bitmap, using the SetMaskingColor() method, is only supported for bitmap containers with a bitmap pixel format of BITMAP_PIXEL_FORMAT_RGB565.

The preview format of the camera control can be set using the Camera::SetPreviewFormat() method. But the value set in this method must be one of the formats supported by the camera device. The formats supported by the camera can be queried using the Camera::GetPreviewFormat() method.

## Related Recipe

- Add a Form to a Frame-based App

## Recipe 4.5: Record Audio from the Microphone or Audio Input Device

### Problem Description

You want to record audio from the microphone and save the recording to a file.

### The Recipe

The following configuration is required for this recipe:

| | |
| --- | --- |
| Namespaces used: | Osp::UI, Osp::Media, Osp::UI::Controls |
| Header files to #include: | FUi.h, FMedia.h |
| Required libraries: | FUi, FMedia |
| Required privilege level: | Normal |
| Required privilege groups: | RECORDING |

The AudioRecorder class records audio data from an input source to storage. The selection of input device source depends on the current device status. For example, if a headset mic device is connected, it is automatically selected as an input source. The audio recording format, the maximum recording time, and the maximum recording size can be set using the methods in this class.

Having created an AudioRecorder instance, you will want to implement a listener to be informed of appropriate events during the recording process. Osp::Media::IAudioRecorderEventListener interface class is available for this. When inheriting from this class you will be required to implement methods that will be called in your application to inform of recording events.

This recipe will show how to create one such listener and how this can be combined with an AudioRecorder instance to record audio to a file. First, we will create an audio recorder listener. This will be tied to the AudioRecorder instance to inform our application of AudioRecorder events:

```cpp
#include <FBase.h>
#include <FMedia.h>

class MyAudioRecorderListener:
    public Osp::Media::IAudioRecorderEventListener
{
public:
    void OnAudioRecorderStopped(result r);
    void OnAudioRecorderCanceled(result r);
    void OnAudioRecorderPaused(result r);
    void OnAudioRecorderStarted(result r);
    void OnAudioRecorderEndReached(
        Osp::Media::RecordingEndCondition
        endCondition);
    void OnAudioRecorderClosed(result r);
    void OnAudioRecorderErrorOccurred(
        Osp::Media::RecorderError r);
};
```

Each method declared above will be implemented for the MyAudioRecorderListener class.

Let’s now create the AudioRecorder instance and provide it with a handle to our listener.

```cpp
result
MyApp::CreateAudioRecorder(void)
{
    result r = E_SUCCESS;

    pAudioRecorder = new AudioRecorder();
    pListener = new MyAudioRecorderListener;

    r = pAudioRecorder->Construct(*pListener);
    if (!IsFailed(r))
    {
        r = pAudioRecorder->CreateAudioFile(path, true);
        if (!IsFailed(r))
        {
```
