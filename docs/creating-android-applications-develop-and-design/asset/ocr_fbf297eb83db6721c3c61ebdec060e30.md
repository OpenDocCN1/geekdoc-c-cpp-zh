```
```java
    mCursor.close();
if(mPlayer != null) {
    mPlayer.stop();
    mPlayer.release();
}
}
```
```

I must be careful, because an incorrect data source ID or bad media file could leave either of these pointers null, which would crash the service quite handily when I try to shut them down.

# INTERRUPTIONS

When you're writing music software for Android devices, it's vitally important that you remember that the hardware on which your software is running is, in fact, a phone. This means you'll need to watch out for several things.

+   - **Audio focus.** You'll need to use the *AudioManager* class (introduced in Android 2.2) to register an audio focus listener, because other applications may want to play alerts, navigational directions, or their own horrible music. This is vital to making an Android music playback application play nice with the rest of the system.
+   - **Controls built into headphones.** You'll want your service to register to receive headset button intents through your manifest (or at runtime when your service is started). At the very least, set your service up to pause when the headset control is clicked.
+   - **Phone calls.** By watching the phone's call state either through the *TelephonyManager* or with the audio focus tools, you *absolutely must* watch for incoming phone calls. You must stop all audio when the phone rings. Nothing will enrage your users (and hurt your ratings) more than not accommodating phone calls.