# ### ONPAUSE()

onPause is the first method called by the system as your application is leaving the screen. If you have any processes or loops (animations, for example) that should be running only while your activity is onscreen, the onPause method is the perfect place to stop them. onPause will be called on your activity if you've launched another activity over the one you're currently displaying.

Keep in mind that if the system needs resources, your process could be killed anytime after the onPause method is called. This isn't a normal occurrence, but you need to be aware that it could happen.

The onPause method is important because it may be the only warning you get that your activity (or even your entire application stack) is going away. It is in this method that you should save any important information to disk, your database, or the preferences.

Once your activity has actually left the screen, you'll receive the next call in the activity lifecycle.

# ### ONSTOP()

When Android calls your onStop method, it indicates that your activity has officially left the screen. Further, onStop is called when the user is leaving your activity to interact with another one. This doesn't necessarily mean that your activity is shutting down (although it could). You can only assume that the user has left your activity for another one. If you're doing any ongoing process from within your activity that should run only while it's active, this method is your chance to be a good citizen and shut it down.

# ### ONDESTROY()

onDestroy is your last method call before oblivion. This is your last chance for your activity to clean up its affairs before it passes on to the great garbage collector in the sky.

Any background processes that your activity may have been running in the background (fetching/parsing data, for example) must be shut down on this method call.

However, just because onDestroy is called doesn't mean that your activity will be obliterated. So if you have a thread running, it may continue to run and take up system resources even after the onDestroy method is called.