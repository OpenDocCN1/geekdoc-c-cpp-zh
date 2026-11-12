```
~~~java
    startService(serviceIntent);
}
else if(v.getId() == R.id.stop_service){
    stopService(serviceIntent);
}
}
~~~
```

This, again, is pretty simple. The buttons, when clicked, will call this onClick method. Depending on the view that actually got the click, I'll either start or stop the service.

# ## SPINNING UP THE SERVICE

Right now, if you were to run the code as it stands, you'd press the button, the service would start, and...nothing whatsoever would happen. Let me show you how to change that.

I want to be notified by the system every time someone takes a picture with the device's camera. To do this, you'll have to register an observer with Android's media ContentProvider. Switching back to the PhotoListenerService.java file, register for media notifications in the service's onCreate method:

```
~~~java
@Override
public void onCreate(){
    super.onCreate();
    getContentResolver().
    registerContentObserver(
        MediaStore.Images.Media.EXTERNAL_CONTENT_URI,
        true,
        observer);
}
~~~
```

To register a content observer, I'll need to provide a Uniform Resource Identifier (URI). In this case, I'll use the constant URI for all photos saved on the external SD card. This constant is declared in the MediaStore. The second parameter is me