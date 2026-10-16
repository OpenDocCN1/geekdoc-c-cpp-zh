also use a finger with your touch device or use the mouse because the `InputDeviceTypes` property has been configured accordingly.

![](bbox=[0.105, 0.107, 0.894, 0.512])

Figure 32.29

# Pickers for Reading and Writing Strokes

As previously mentioned, the `InkCanvas` control also supports accessing the created strokes. These strokes are used with the following sample to store it in a file. The file is selected using the `FileSavePicker`. The method `OnSave` is invoked on clicking the `Save AppBarButton` that was created previously. The `FileSavePicker` is the UWP variant of the `SaveFileDialog`. With Windows 8, this picker has been full screen, but now with UWP, where it can be contained in smaller windows, this picker has changed as well.

First, the `FileSavePicker` is configured by assigning a start location, a file type extension, and a filename. At least one file type choice needs to be added to allow the user to select a file type. Invoking the method `PickSaveFileAsync`, the user is asked to select a file. This file is opened to transactional write invoking the method `OpenTransactedWriteAsync`. The strokes of the `InkCanvas` are stored in the `StrokeContainer` of the `InkPresenter`. The strokes can be directly saved to a stream with the `SaveAsync` method (code file `ControlsSamples/Views/InkSample.xaml.cs`):

```
private const string FileTypeExtension = ".strokes";
public async void OnSave()
```