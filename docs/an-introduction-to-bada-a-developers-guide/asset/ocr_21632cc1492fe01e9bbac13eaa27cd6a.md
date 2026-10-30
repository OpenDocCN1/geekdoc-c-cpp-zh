Now, we want to check whether the format and resolution of the video are supported. In our snippet, the maximum resolution should be the last element in the list we get directly from the camera. With regard to pixelFormat, we can assume that each device has at least one format, so we select the first element.

```
IList* pPreviewResolutionList = null;
IList<T<PixelFormat>*> pPreviewFormatList = null;

pPreviewResolutionList = pCamera->
    GetSupportedPreviewResolutionListN();

// supported max resolution
Dimension* pPreviewResolution =
    (Dimension*)pPreviewResolutionList->GetAt(
        pPreviewResolutionList->GetCount()-1
    );

pPreviewFormatList = pCamera->GetSupportedPreviewFormatList();
PixelFormat pixelFormat;
pPreviewFormatList->GetAt(0, pixelFormat);    //first element

pCamera->SetPreviewResolution(*pPreviewResolution);
pCamera->SetPreviewFormat(pixelFormat);

resolution = *pPreviewResolution;    //store in member variable
format = pixelFormat;
```

Then we invoke the preview of the camera by issuing the StartPreview() method. Its first argument holds a data buffer for the camera preview. The second argument is a bool, where true means to trigger the callback function OnCameraPreviewed(). False would disable this callback function.

```
pCamera->StartPreview(&bufferInfo, true);
```

If you are using the camera preview, make sure that you turn it off when your app is terminating in the OnTerminating() method as shown below:

```
result
Form1::OnTerminating(void)
{
    result r = E_SUCCESS;
    if(r = pCamera->GetState() == CAMERA_STATE_PREVIEW)
    {
        pCamera->StopPreview();
        pCamera->PowerOff();
        delete pCamera;
    }
    return r;
}
```