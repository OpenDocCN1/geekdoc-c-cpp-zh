We called Player::OpenFile asynchronously, so we need to actually start the audio player when we know the content is successfully opened. The method to use is the OnPlayerOpened method of IPlayerEventListener:

```
void
AudioPlayerForm::OnPlayerOpened(result r)
{
    // The content is successfully opened, start playing
    pAudioPlayer->Play();
}
```

When the audio has finished playing the OnPlayerEndOfClip method is invoked. We'll close the player in this method. pAudioPlayer will be deleted in our form's destructor.

```
void
AudioPlayerForm::OnPlayerEndOfClip()
{
    pAudioPlayer->Close();
}
```

# Other IPlayerEventListener methods

In our example we implemented two IPlayerEventListener methods: OnPlayerOpened and OnPlayerEndOfClip. IPlayerEventListener also contains a number of other methods, listed in Table R4.1.

# Table R4.1 Other IPlayerEventListener methods

| Method | Description |
|---|---|
| OnPlayerInterrupted | Called when the player is interrupted as a result of an event such as receiving a call. The player will be automatically stopped. Note this handler is only invoked when the player is interrupted while playing some content |
| OnPlayerReleased | Called when the external event that interrupted the player in OnPlayerInterrupted has completed. It is the responsibility of the application to start the sound playing again by calling the Play() method of Player |
| OnPlayerBuffering | Called to notify the application that streaming data is being buffered. You could update your user interface at this point to let the user know why audio playback is not as smooth |
| OnPlayerErrorOccured | This method is sent a Media::PlayerErrorReason specifying errors such as out of memory or connection errors with streaming data |
| OnPlayerSeekCompleted | Called when moving to a certain position in audio or video is completed |