If you need a temporary holding pen for data that may span many activities, a data member that's part of the Application can be a convenient place to store it. You must be very careful about adding data to the Application. Any single component declared in your manifest, from the simplest BroadcastReceiver to the most complex activity, will, before it's created by the system, first create your Application object. This means you must make the Application's onCreate method run as fast as you possibly can.

# ACCESSING THE APPLICATION

All your broadcast receivers, services, activities, and content providers have a method called getApplication provided to them by the appropriate superclass. When invoked, getApplication will return a pointer to your Application object if you specified one in the manifest. Getting access to it, now that you've declared and created the class, is as simple as calling getApplication and casting the returned object to an instance of your own pointer. Here's what it looks like:

```
~~~
SampleApplication myApplication = (SampleApplication)
getApplication();
~~~
```

That's all there is to it. You can add public data members or context-sensitive methods to your own version of the Application, and with one call all your components will have access to the same object, like so:

```
~~~
public class SampleApplication extends Application{
    public String username;
    public void onCreate(){
        super.onCreate();
    }
}
~~~
```