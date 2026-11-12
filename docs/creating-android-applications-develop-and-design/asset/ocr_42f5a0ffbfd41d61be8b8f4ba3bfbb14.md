so once you set it, it can’t be changed. This is how the Android SDK forces you to use a new activity for each screen, because each time you want to change your root content view, you’ll need a different activity.

# TELLING ANDROID ABOUT YOUR FRIENDLY NEW ACTIVITY

The Android system needs to know where to find your new activity when it comes time to launch and launch it.

+   1. Open up the AndroidManifest.xml file in Eclipse.
+   2. Add the following line inside the <application> tag and directly after the </activity> closing tag of the previous declaration:

```
<activity android:name=".NewActivity"/>
```

This little line tells the system where to find the new activity in your application package. In the case of my demo, the class loader knows to look for the activity at com.haseman.peachPit.NewActivity.

Next, you’ll need to put a file there for it to find.

# CREATING THE NEW ACTIVITY CLASS

There are several ways to create a new activity, but here is the easiest way to do it in Eclipse.

+   1. Right-click (or Control-click) the package name you’ve chosen (mine is com.haseman.peachPit).
+   2. Select New, then select Class.
+   3. Give the class a name in the dialog.

A name is enough to create a new file. The file will be saved in your main package under the name you specified. In my demo, it is in my project under src/com/haseman/peachPit/NewActivity.java.

Now that you have a class that extends an object, you’ll need to switch it over to extend an activity.