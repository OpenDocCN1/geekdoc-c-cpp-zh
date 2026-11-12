
## REMEMBER THE MAIN THREAD!

Just because you’re running in a service doesn’t mean you’re off the main thread! The service’s `onCreate` method will be called on the main thread. If you need to do any heavy lifting, consider using an `AsyncTask` or a `Handler+Looper` pattern, or instead of doing a normal service, use an `IntentService` to process heavy data off the main thread. Further, there are certain actions (like recording audio) that you can initiate only from the main thread. It’s 10 a.m., do you know where your threads are?

## KEEPING YOUR SERVICE RUNNING

The `startForeground` method is your chance to strike a clever deal with Android. The system agrees that after you call this method and until you call `stopForeground`, it will not kill off your service. In exchange, you must provide an icon and view to be shown to the user in the top bar by handing it a `Notification` object. This contract allows long-running, essential, and intensive services (such as music playback or photo uploading) to run without fear of extermination. At the same time, the user is aware of why their phone might be a little sluggish.

## SHUT IT DOWN!

At some point, the party will end and it’ll be time to clean up. This can happen because your service called `stopSelf` or because another component called `Context.stopService`. Here’s the teardown portion of the lifecycle:

- `onDestroy` is your chance to cancel any running tasks and put away any resource you’ve taken on (for example, media or network tasks). This is also your chance to unregister any `BroadcastReceivers` or `ContentObservers` that you’ve set up to watch for new media.

If you were expecting a many-step shutdown process, I’m afraid you’re going to be disappointed. Because services have no notion of being on top of the screen, there is no need to pause, resume, or do any of the other complex interactions that activities must support.

There are two main ways to communicate with a service: intent broadcasts and binder interfaces. I’m going to show you examples of both and, along the way, let you see two practical tasks for a service. There are, in fact, many more ways you can communicate with your services. But in my experience, these are the two most useful. As always, check the documentation if neither of these approaches feels quite right for you.

## INTENT-BASED COMMUNICATION

Imagine two workers in different rooms who can only communicate with each other by email. These emails can contain attachments and other pieces of data. The two workers must get through their day using only this one method of communication. As you might imagine, this can be an efficient and functional way to get a multitude of things done, as long as they don’t have to say too much to each other.

This is, in a sense, exactly what *intent-based communication* with services would look like translated to real life. The service is started with an intent; when it completes its task or something that it’s waiting for occurs, it sends a broadcast intent alerting anyone listening that a particular task is finished. You saw one example of this in Chapter 4 when I was downloading images using an intent service. Let me show you one more.

The following example is one of the best examples of intent-based communication that I can give you in this printed form. I’ll create all the pieces required for a new service that runs, with a notification, in the foreground. I use Android’s ContentProvider to listen for and acquire the location of new photographs as they are taken. This code will alert you when any new picture is snapped, regardless of the application used to do it. What you do with the photograph, I’ll leave to your boundless imagination.

## AUTO IMAGE UPLOADING

One of my favorite features of the Google+ Android app is its ability to automatically upload photos in the background. It turns out that with a ContentProvider, Service, and ContentObserver, you can do this quite easily in your own app. My sample service will launch, place itself in the foreground, and trigger a broadcast intent whenever a new photo is taken. You could, in your own code, upload the image or take any number of other actions. Using this technique would involve the following general steps.

- 1. Declare the service.
- 2. Get yourself a service.
- 3. Start the service.
- 4. Spin up the service.
- 5. Go to the foreground.
- 6. Observe when content changes.

Let's get started.

### DECLARING THE SERVICE

You must tell Android where to find the service.

Each service, as you know, must be declared in the manifest. You can add an intent filter for it to respond to (if you want applications other than your own to be able to start it). For my example, this isn't necessary, but it might be something you need to take advantage of later. Here's the single line you'll need to place in your manifest:

```xml
<service android:name="PhotoListenerService"/>
```

### GETTING YOURSELF A SERVICE

Now create the class that extends service.

```java
public class PhotoListenerService extends Service {
    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }
}
```

Since `onBind` is a required method for the `Service` class, it has to be in my class or it won't compile. Now that you've got a service, let's look at how to actually start it.

- 2. With these in place, you can now write code to start and stop the photo listening service. Here's what the updated ServiceExampleActivity now looks like:

```java
public class ServiceExampleActivity extends Activity
        implements OnClickListener {
    /** Called when the activity is first created. */
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        Button btn = (Button)findViewById(R.id.start_service);
        btn.setOnClickListener(this);
        btn = (Button)findViewById(R.id.stop_service);
        btn.setOnClickListener(this);
    }
}
```

Nothing earth-shattering in this listing. I'm retrieving references to the views once they've been built. I set my class to implement the `OnClickListener` interface, which allows me to set the activity itself as the click listener for the two buttons. The above code will not compile until you implement `View.onClick`.

- 3. Implement the `onClick` method:

```java
@Override
public void onClick(View v) {
    Intent serviceIntent = new Intent(getApplicationContext(),
            PhotoListenerService.class);
    if(v.getId() == R.id.start_service){
        startService(serviceIntent);
    }
    else if(v.getId() == R.id.stop_service){
        stopService(serviceIntent);
    }
}
```

This, again, is pretty simple. The buttons, when clicked, will call this `onClick` method. Depending on the view that actually got the click, I'll either start or stop the service.

### SPINNING UP THE SERVICE

Right now, if you were to run the code as it stands, you'd press the button, the service would start, and...nothing whatsoever would happen. Let me show you how to change that.

I want to be notified by the system every time someone takes a picture with the device's camera. To do this, you'll have to register an observer with Android's media ContentProvider. Switching back to the `PhotoListenerService.java` file, register for media notifications in the service's `onCreate` method:

```java
@Override
public void onCreate(){
    super.onCreate();
    getContentResolver().
    registerContentObserver(
        MediaStore.Images.Media.EXTERNAL_CONTENT_URI,
        true,
        observer);
}
```

To register a content observer, I'll need to provide a Uniform Resource Identifier (URI). In this case, I'll use the constant URI for all photos saved on the external SD card. This constant is declared in the MediaStore. The second parameter is me telling Android that I'd like to know when children of that URI are modified. I set it to true because I'll want to know when any of the descendants of the image URI are modified, added, or deleted. Last, I pass in my observer. This is the object whose `onChange` method will be called whenever the ContentProvider is updated. It will register for media updates, but there's still one more method you'll need to define.

### GOING TO THE FOREGROUND

Bringing your service into the foreground protects it from being killed by Android when resources are low.

Implement the `onStartCommand` method of your service as follows.

```java
public int onStartCommand(Intent intent, int flags, int startId) {
    super.onStartCommand(intent, flags, startId);
    lastUpdateTime = System.currentTimeMillis();
    setForegroundState(true);
    return Service.START_STICKY;
}
```

I'm going to record when the service started (more on why that's important in just a second). Last, I return `Service.START_STICKY`, which tells the system that should the service be terminated for memory or performance reasons, I'd like to have it started back up.

I need to write a function to handle creating a notification and moving the service into the foreground. `setForegroundState` is my own method that handles placing the service and removing the service from foreground mode.

```java
private void setForegroundState(boolean enable){
    if(enable){
        Notification n = new Notification(
            R.drawable.icon,
            "Service is uploading all your photos",
                System.currentTimeMillis());
        n.contentView = new RemoteViews(
```
