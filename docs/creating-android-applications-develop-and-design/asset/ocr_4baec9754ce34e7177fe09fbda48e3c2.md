+   4. Add the following highlighted line to the onCreate method of your New Activity class:

```
```java
public void onCreate(Bundle icicle){
    super.onCreate(icicle);
    setContentView(R.layout.new_activity);
}
```
```

setContentView is the method in which you tell Android which XML file to display for your new activity. Now that you've created a new class, string, and layout file, it's time to launch the activity and display your new view on the screen.

# CATCHING KEYS

The simple way to launch your new activity is to have the user press the center key on his or her device. If your phone doesn't have a center key, you can easily modify the following code to accept any key you like. To listen for key events, you'll need to extend the original activity's onKeyDown method. Keep in mind that this is a simple example case. Launching a new activity when the user presses a single key probably isn't a very common use case in practice, but it makes for a good and simple example. Most new activities are started when a user selects a list item, presses a button, or takes another action with the screen.

Here's what your new version of onKeyDown should look like:

```
```java
@Override
public boolean onKeyDown(int keyCode, KeyEvent event){
    if(keyCode == KeyEvent.KEYCODE_DPAD_CENTER){
        //Launch new Activity here!
        return true;
    }
    return super.onKeyDown(keyCode, event);
}
```
```