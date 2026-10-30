The AudioRecorder class records audio data from an input source to storage. The selection of input device source depends on the current device status. For example, if a headset mic device is connected, it is automatically selected as an input source. The audio recording format, the maximum recording time, and the maximum recording size can be set using the methods in this class.

Having created an AudioRecorder instance, you will want to implement a listener to be informed of appropriate events during the recording process. Osp::Media::IAudioRecorderEventListener interface class is available for this. When inheriting from this class you will be required to implement methods that will be called in your application to inform of recording events.

This recipe will show how to create one such listener and how this can be combined with an AudioRecorder instance to record audio to a file. First, we will create an audio recorder listener. This will be tied to the AudioRecorder instance to inform our application of AudioRecorder events:

```
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
```

Each method declared above will be implemented for the MyAudioRecorderListener class.

Let’s now create the AudioRecorder instance and provide it with a handle to our listener.

```
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
```