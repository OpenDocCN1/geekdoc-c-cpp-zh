Music playback, in general, revolves around the MediaPlayer class. This is in a sense very similar to what you've just done with the video view (except you don't need a View object to render into).

Media players, if used to play music, should end up in their own services, with one notable exception: games and application sound effects. Building a sound effect example will make for a very simple way to get into the basics of audio playback.

# MEDIAPLAYER AND STATE

You do not simply walk into Mordor. Similarly, you do not simply run about playing things willy-nilly. It requires care, attention to detail, and an understanding of the media player's states. Here they are, in the order you're most likely to encounter them:

+   - Idle. In this state, the MediaPlayer doesn't know anything and, consequently, cannot actually do anything. To move on to the initialized state, you'll need to tell it which file it's going to play. This is done through the setDataSource method.
+   - Initialized. At this point, the media player knows what you'd like it to play, but it hasn't acquired the data to do so. This is particularly important to understand when dealing with playing remote audio from a URL. Calling prepare or prepareAsync will move it into the prepared state. It will also load enough data from either the file system or the Internet to be ready for playback.
+   - Prepared. After calling prepare or prepareAsync (and getting a callback), your media player is ready to rock! At this point, you can call seek (to move the playhead) or start (to begin playback).
+   - Playing. Audio is pumping, people are dancing (OK, maybe not), and life is good. In this state, you can call pause to halt the audio or seek to move the play position. You end the party by calling stop, which will move the media player back to the initialized state.

Just because you've run out of media to play doesn't mean your player drops into the idle state. It will keep the current file loaded if you want to call start (which will restart the audio from the beginning) or seek (to move the playhead to a particular place). Only when you call stop or reset does the MediaPlayer clear its buffers and return to the initialized state, ready for you to call prepare again.