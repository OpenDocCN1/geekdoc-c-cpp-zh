# A DIFFERENT WAY

It’s worth noting, again, that I’ve taken the harder of two routes here. Instead of querying the content provider for the exact media path, I could build a URI for the media in question and hand it off instead. I’ve taken what may be a slightly more complex route to playback only so that when you’d like to get to the file itself, you’ll know how.

+   3. When I’m sure the cursor is valid and contains the data for a song to play, I can reset the player (in case it was already playing something else), set the data source for it, and tell the media player to prepare. Once these methods are done, the media player is ready to start playback.

With that, your service is ready to go when the activity calls play.

# PLAY TIME

Now that the service has a data source and is prepared, the activity can call play, which will trigger the following code to run:

```
```java
private void play(){
    if(mPlayer != null){
        mPlayer.start();
        setForegroundState(true);
    }
}
```
```

You’ll need to start media playback and make sure the service switches to running in the foreground. setForegroundState is a method I defined back in Chapter 6 that places an icon in the notification screen. If you need a refresher on how to put services into foreground mode, review Chapter 6 or look at the sample code for this chapter.