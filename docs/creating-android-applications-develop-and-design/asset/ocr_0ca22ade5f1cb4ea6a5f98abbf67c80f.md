There are a few key points in your manifest that you need to pay attention to before you consider producing a release build to go to market. You'll need to make sure your application isn't debuggable (not so much an issue with newer versions of the Android client). You'll also want to make sure your package name is unique and consistent in each subsequent version. Last, there are two fields to pay attention to when upgrading an existing application. Let's take a closer look at all three.

# ## PREVENTING DEBUGGING

Shipping your application out the door with debugging enabled will allow anyone with a micro USB cable to step through lines of code in your app, look at the contents of variables, and do other things that no security-aware engineer would like to have happen. The debugging flag is turned off by default, but if you've turned it on, it will appear in the application portion of the manifest:

```
```xml
<application
    android:icon="@drawable/ic_launcher"
    android:label="@string/app_name"
    android:debuggable="true">
```
```

When the application ships, make sure that you either remove the line entirely or set the following:

```
```xml
android:debuggable="false"
```
```

# ## NAMING THE PACKAGE

The package you declare in your manifest can, for the most part, contain almost any string you fancy. I've highlighted one from a previous example here:

```
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.haseman.layouts"
    android:versionCode="1"
    android:versionName="1.0">
```
```