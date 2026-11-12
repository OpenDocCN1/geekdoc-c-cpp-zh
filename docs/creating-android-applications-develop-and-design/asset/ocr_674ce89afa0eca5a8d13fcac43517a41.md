suffice so I can pass null for the last parameter. Theoretically, the cursor should contain exactly one image. Here's how I process the cursor coming back from the ContentProvider:

```
```
lastUpdateTime = System.currentTimeMillis();
if(cursor.moveToFirst()){
    Intent i = new Intent(ACTION_PHOTO_TAKEN);
    int dataIDX = cursor.getColumnIndex(MediaStore.Images.Media.DATA);
    i.putExtra("path", cursor.getString(dataIDX));
    sendBroadcast(i);
}
```
```

![](bbox=[0.73, 0.23, 0.95, 0.53])

> **TIP:** Uploading photos: Normally, instead of calling sendBroadcast, I'd spin up another service (or an AsyncTask) to upload the photo to my favorite photo-sharing service. These services change so often that it's probably not worth spelling out exactly how to accomplish such a thing for Twitter, Flickr, Tumblr, or Imgur. If you want to implement your own, use the photo-downloading IntentService from Chapter 4 as a framework and go from there.

Now that I have the cursor, I can set the new lastUpdateTime. This will ensure that this current picture will not show up in subsequent observer-fired queries. Instead of starting an upload, I'm just sending an alert that a photo was taken and where you can find that new file. I then move the cursor to its initial position and make sure (by checking to see if it returns true) that there is actually a piece of data to find. Next, I'll get the column index for the data column. Last, I'll retrieve the path from the cursor and add it as an extra to my new intent. Last, I broadcast the existence of the photo for anyone who might be listening for it.

It's important to call cursor.close on every cursor you get back from a Content Provider. Otherwise, the system will throw errors at you for leaking memory.