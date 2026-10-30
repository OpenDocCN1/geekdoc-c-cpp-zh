Our example consists of the following steps:

+   1. Create the new Media::Player object.
+   2. Construct the Media::Player object with the form as the IPlayerEventListener.
+   3. Open the audio file using Media::Player::OpenFile.
+   4. Play the audio.
+   5. Close the Media::Player.

Let's see how we do this in code:

```
// Create and construct the media player
pAudioPlayer = new Player();
pAudioPlayer->Construct(*this);

// Open the audio filed stored locally on the device
// The first parameter specifies the path
// The second parameter specifies whether we should open the file
// synchronously or asynchronously. We pass true for asynchronously
pAudioPlayer->OpenFile(L"/Res/bell_effect.wav", true);
```

You have a choice of three methods to choose the audio or video content: OpenFile to open a file stored locally on the device, OpenUrl to open a file to stream remotely from a server and OpenBuffer to play content from a ByteBuffer. Each of these methods can be used synchronously or asynchronously. When dealing with small files stored locally on the device, you will probably choose to open the content synchronously, whereas with remote content or large files stored locally, it makes more sense to open the content asynchronously, to ensure that your application stays responsive while the media content is being opened.

In our example we're using the form as the listener, so we need to set up our form to derive from IPlayerEventListener to receive and handle media player events:

```
class AudioPlayerForm :
public Osp::UI::Controls::Form,
public Osp::UI::IActionEventListener,
public Osp::Media::IPlayerEventListener,
```

We need to implement the following methods of IPlayerEvent Listener:

```
virtual void OnPlayerBuffering(int percent);
virtual void OnPlayerEndOfClip();
virtual void OnPlayerErrorOccurred(
Osp::Media::PlayerErrorReason r);
virtual void OnPlayerInterrupted();
virtual void OnPlayerOpened(result r);
virtual void OnPlayerReleased();
virtual void OnPlayerSeekCompleted(result r);
```