adapter in the Windows system. If this information is not available, then the default adapter winvideo can be used. This adapter will automatically be directed to the video source understood by Windows. More information about this particular device can be obtained through the function imaqhwinfo().

Once the device is configured, the image can be previewed using the preview() function to create a typical “viewfinder” window. The actual image can be acquired directly into a local variable using the function getsnapshot(). Multiple snapshots can be used by employing standard looping techniques. The function delete() helps in freeing some memory once the acquisition is done. The following is a typical code snippet for acquiring an image:

```
x = videoinput('winvideo',1);
imaqhwinfo(x)
preview(x)
y = getsnapshot(x);
imshow(y)
delete(x)
```

The result of the second line is the following text:

```
ans =

AdaptorName: 'winvideo'
DeviceName: 'Labtec webcam plus'
MaxHeight: 288
MaxWidth: 352
NativeDataType: 'uint8'
Totalsources: 1
VendorDriverDescription: 'Windows WDM Compatible
Driver'
VendorDriverVersion: 'DirectX 9.0'
```

The remaining lines will display two images, one for the preview and the other one for the actual acquisition allocation.

The basic data structure in MATLAB is the array; an ordered set of real or complex elements. This object is naturally suited to the representation of images, real-valued ordered sets of color or intensity data.

MATLAB stores most images as two-dimensional arrays (i.e., matrices) in which each element of the matrix corresponds to a single pixel in the displayed image. (Pixel is derived from picture element and usually denotes a single dot on a computer display.) For example, an image composed