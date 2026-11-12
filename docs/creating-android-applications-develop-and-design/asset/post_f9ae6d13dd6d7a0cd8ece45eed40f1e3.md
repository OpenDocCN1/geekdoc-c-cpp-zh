
Typically, an Android application is a collection of activities, broadcast receivers, services, and content providers. The Application class is the glue that binds all these disparate pieces into a singular, unified entity. Every time a content provider, activity, service, or intent receiver in your manifest is initialized, an Application class is also spun up and available to it.

## THE DEFAULT APPLICATION DECLARATION

Looking in the AndroidManifest.xml file, you'll see a typical Application declaration that looks like the following:

```xml
<application android:icon="@drawable/icon"
    android:label="@string/app_name">
<!--Activities, Services, Broadcast Receivers, and Content Providers -->
</application>
```

Here you can see the `<application>` tag. This part of the manifest typically contains information relevant to your application at large. `android:icon` tells the system what icon to display in the main application list. `android:label` in this case refers to another entry in the `strings.xml` file you were editing earlier.

## CUSTOMIZING YOUR OWN APPLICATION

Adding your own application is very similar to the steps you've already gone through to add a new activity.

- 1. Add a name field to the existing `AndroidManifest.xml` declaration.
- 2. Create a new class in your package that extends the `Application` class.
- 3. Profit!

Let's go over steps 1 and 2 in depth. You're on your own for step 3.

## THE NAME

When it comes to the manifest, `android:name` refers not to the name of the object being described, but to the location of the class in your Java package. The `Application` declaration is no exception. Here's what the opening tag of the application should look like with the new declaration:

If you need a temporary holding pen for data that may span many activities, a data member that's part of the Application can be a convenient place to store it. You must be very careful about adding data to the Application. Any single component declared in your manifest, from the simplest BroadcastReceiver to the most complex activity, will, before it's created by the system, first create your Application object. This means you must make the Application's onCreate method run as fast as you possibly can.

## ACCESSING THE APPLICATION

All your broadcast receivers, services, activities, and content providers have a method called getApplication provided to them by the appropriate superclass. When invoked, getApplication will return a pointer to your Application object if you specified one in the manifest. Getting access to it, now that you've declared and created the class, is as simple as calling getApplication and casting the returned object to an instance of your own pointer. Here's what it looks like:

```
SampleApplication myApplication = (SampleApplication)
getApplication();
```

That's all there is to it. You can add public data members or context-sensitive methods to your own version of the Application, and with one call all your components will have access to the same object, like so:

```
public class SampleApplication extends Application{
    public String username;
    public void onCreate(){
        super.onCreate();
    }
}
```

## THE VIEW CLASS

No, this isn't a television show where several women debate the merits of common culture. The View class is the superclass for all the Android display objects. Each and every user interface (UI) class from the simple ImageView to the mighty RelativeLayout all subclass from this same object. In this section, you'll learn the basics of creating, adding, and modifying your existing layouts using Java code and XML. You'll also learn to create your own custom view. A view, at its very core, is simply a rectangle into which you can display something. Subclasses take many different forms, but they all need, simply, a space to show something to the user.

### CREATING A VIEW

Creating a new view is something you've already done. In Chapter 1, you added a view to an XML layout file as part of exploring how to launch a new activity. At the time, I told you we'd get into the specifics of how these views were created and modified, and, well, now's the time! Let's take a look at the default views generated for you automatically when you create a new Android project.

#### VIEWS IN XML

Here's what the default XML layout looks like in a new project:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    >
<TextView
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:text="@string/hello"
    />
</LinearLayout>
```

#### HEIGHT AND WIDTH ARE REQUIRED

For now, it’s important to note that every single layout must have a value set for both its height and its width. Android may not fail to compile if you do not specify these values (as they could be updated at runtime), but if it starts to draw your views and the system height and width values are missing, then your application will crash.

Question: Which of the two elements (LinearLayout and TextView) in this default XML layout are views?

Answer: Both.

All visual objects onscreen subclass from the View class. If you go high enough in the inheritance chain, you’ll find an “extends View” somewhere.

In the default XML layout, the Android tools have added a simple TextView contained inside a LinearLayout. When displayed onscreen, the contents of the hello string will appear by default in the upper-left corner of the screen. I’ll discuss how to position visual elements onscreen later in this chapter.

To display the XML layout onscreen, you need to call the setContentView() method and pass the name of the layout to the activity.

In Eclipse, your code editor, it should look like this:

```java
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);
}
```

#### VIEWS IN JAVA

Anything you can lay out or build in XML, you can lay out and build also within the Java code itself; it’s just more complex. It’s important, however, to understand what Android is doing as it inflates and builds your layouts.

Here’s what the Java code looks like to build the exact same user interface that Android generates for you in XML when you create a new project:

```java
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(buildLayouts());
}

public View buildLayouts(){
    LinearLayout topView =
        new LinearLayout(getApplicationContext());
    LayoutParams topLayoutParams =
        new FrameLayout.LayoutParams
        (LayoutParams.MATCH_PARENT,
        LayoutParams.MATCH_PARENT);
    topView.setLayoutParams(topLayoutParams);
    TextView textView =
        new TextView(getApplicationContext());
        LinearLayout.LayoutParams textLayoutParams =
            new LinearLayout.LayoutParams(
            LayoutParams.WRAP_CONTENT,
            LayoutParams.MATCH_PARENT);
        textView.setLayoutParams(textLayoutParams);
        textView.setText(R.string.hello);
        topView.addView(textView);
        return topView;
}
```
