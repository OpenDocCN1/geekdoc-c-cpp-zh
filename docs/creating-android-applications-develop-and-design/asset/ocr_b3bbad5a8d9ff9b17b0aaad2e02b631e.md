# MOVIES

Movie playback on an Android device boils down to the VideoView class. In this section, I'll use a simple example application that will play through every video saved on a phone's SD card. Here is the general process:

+   - I'll use the ContentProvider (something you'll remember from our brief discussion in Chapter 6 when we uploaded the most recent photo) to request every video saved to the user's external card.
+   - After loading a Cursor (Android's query result data object) with all the device's videos, I'll need a method to play the next one.
+   - I'll set up an activity as a listener so that when video playback is complete, I can call my playNextVideo method and move on to the next video in the cursor.
+   - Last, I'll clean up after my cursor when the user leaves the playback screen.

Before I can do any of these things, however, I need to place a VideoView on my main layout to work with.

# ADDING A VIDEOVIEW

Placing a VideoView onscreen is as simple as adding it to your XML layout. Here's what my main.xml file now looks like:

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/
    apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >
<VideoView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/my_video_view"
    />
</LinearLayout>
```