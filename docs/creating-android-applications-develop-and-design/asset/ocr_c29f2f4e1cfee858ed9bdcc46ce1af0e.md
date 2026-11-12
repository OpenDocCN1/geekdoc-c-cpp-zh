I now have a configured, yet very simplistic, video player. You'll most likely want to have visual onscreen controls. Android's VideoView allows you to implement and set up a MediaController for the VideoView class. If you're looking to go further into video playback after this chapter, this would be an excellent place to start.

# ### GETTING MEDIA TO PLAY

Now that my video view is ready to roll, I can start hunting for things for it to actually play. For this simple example, I'm going to play every video on the device one after another until they're all finished. To achieve this, I'll use Android's media ContentProvider (accessed with a call to getContentResolver). I'll show you the code and then dig into some specifics. Here's what onCreate looks like with the new code to fetch a cursor with all the media objects:

```
```java
Cursor mediaCursor = null;
VideoView videoView = null;
int dataIdx = 0;
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);
    videoView = (VideoView)findViewById(R.id.my_video_view);
    videoView.setOnCompletionListener(this);
    String projection[] = new String[] {Video.Media.DATA};
    mediaCursor =
            getContentResolver().query(
                    Video.Media.EXTERNAL_CONTENT_URI,
                    projection, null, null, null);
    if(mediaCursor != null && mediaCursor.getCount() > 0){
        dataIdx = mediaCursor.getColumnIndex(Video.Media.DATA);
        playNextVideo();
    }
}
```
```