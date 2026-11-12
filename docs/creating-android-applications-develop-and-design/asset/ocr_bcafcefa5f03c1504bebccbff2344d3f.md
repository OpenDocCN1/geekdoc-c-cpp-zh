# LOADING AND PLAYING MEDIA

At this point, you have a video view, a cursor full of media to play, and a listener configured to tell you when media playback is finished. Let’s put the final piece into the game, the code in playNextVideo:

```
```java
private void playNextVideo(){
    mediaCursor.moveToNext();
    if(mediaCursor.isAfterLast()){
        Toast.makeText(getApplicationContext(),
            "End of Line.", Toast.LENGTH_SHORT).show();
    }
    else{
        String path = mediaCursor.getString(dataIdx);
        Toast.makeText(getApplicationContext(),
            "Playing: "+path, Toast.LENGTH_SHORT).show();
        videoView.setVideoPath(path);
        videoView.start();
    }
}
```
```

![](bbox=[0.0, 0.656, 0.257, 0.868])

My first task is to move the cursor to the next piece of media and make sure we haven't run out of stuff to play. When I know I've got a valid row from the cursor, I can tell the video view what it should render next. Video views can accept both a path defined as a string as well as the URI for a piece of media declared in the content provider. As I mentioned earlier, the data column of the cursor contains the file path to the media itself. I'll pull this out of the Cursor, hand it off to the video view, and then start playback.

> **TIP:** You’re not limited to just file paths—you can hand the video view a URL, and it will query and play the media found there.