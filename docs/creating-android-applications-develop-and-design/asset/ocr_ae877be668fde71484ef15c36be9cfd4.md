Make sure, basically, that the data you’re moving with the AsyncTask pertains to only one activity, because your task generally shouldn’t span more than one. You can pass it between activities if the screen has been rotated, but this can be tricky. There are a few cases when it’s not a good idea to use an AsyncTask:

+   - Any acquired data that may pertain to more than one activity shouldn’t be acquired through an AsyncTask. Both an image that might be shown on more than one screen and a list of messages in a Twitter application, for example, would have relevance outside a single activity.
+   
+   - Data to be posted to a web service is also a bad idea to put on an AsyncTask for the following reason: Users will want to fire off a post (posting a photo, blog, tweet, or other data) and do something else, rather than waiting for a progress bar to clear. By using an AsyncTask, you’re forcing them to wait around for the posting activity to finish.
+   
+   - Last, be aware that there is some overhead for the system in setting up the AsyncTask. This is fine if you use a few of them, but it may start to slow down your main thread if you’re firing off hundreds of them.

You might be curious as to exactly what you should use in these cases. I’m glad you are, because that’s exactly what I’d like to show you next.