
### GeoPoints

Google, in its not-so-infinite wisdom, decided that GeoPoints for the map view should not accept latitude and longitude values in degrees like every other API in the SDK. Instead, they take them in 1e6 values. This means, simply, that you must multiply any latitude or longitude value you wish to reference in the map view by 1e6 before handing off. Interesting map errors will result if you forget this step.

### WRAPPING UP

In this chapter, I showed you the very basics for finding a device's location and displaying a map onscreen. If you're looking to go further into this topic, you should explore map overlays through the `OverlayItem` class. Overlays let you point out specific locations (addresses, businesses, or cat pictures) to your users.

As always, be very careful what kind of location services you use, especially while the user is not in your application. Nothing will drain a user's battery faster—and make them angrier—than heavy locational lookups in the background. If you're planning a very location-heavy application, be sure to do LOTS of battery-draw testing before you release it. Your users and your application's ratings will be much happier for it.

## 10 TABLETS, FRAGMENTS, AND ACTION BARS, OH MY

![](img/47ad0ac10bf11125744ef22c945d3099_236_0.png)

With the release of Honeycomb and Ice Cream Sandwich, Google has introduced a totally new form factor to the Android landscape. In Gingerbread and earlier, Google had sought to handle only small handset screens. With these new versions of Android, you now must deal with the much larger screens of tablets.

Google has introduced the concept of the fragment (to handle the extra screen real estate and to maintain compatibility with smaller, phone-sized screens) and the action bar (to replace the options menu).

Fragments, conceptually, are like activities with a slightly more complex lifecycle. They can be given a screen to themselves if there isn't much room, or they can be placed with many other fragments on a larger tablet screen. An activity can contain any number of fragments. In this way, the Android SDK allows you to expand and collapse the views in your application to take advantage of more and less screen space. There is one thing that the activity can do that the fragment cannot—namely, the activity can register for intents in the manifest; fragments rely on their host activity to pass on launch information. Further, it's important to implement fragments such that they are totally unaware of what other fragments are visible. This becomes important, because you'll want to change that configuration depending on how much space you have.

If you're planning on coding along with me in this chapter, make sure you have a project that is set to version 3.0 or higher of the Android SDK (API Level 11 or greater).

### THE LIFECYCLE OF THE FRAGMENT

Fragments have fairly complex lifecycles. There are many methods to explore, but onCreateView must be implemented for the fragment to appear onscreen. onCreateView is your fragment's one chance to create a view to display onscreen. If you fail to return a view to the system, your application will crash and burn.

Here is the startup lifecycle; the methods are listed in the order the system will call them:

- onAttach. This is called when your fragment is attaching to an activity.
- onCreate. This is called when the fragment is being initialized. This is a great place to initialize any variables you'll need later.
- onCreateView. This is your opportunity to create and return the fragment's root view. This is the first method that will be called if your fragment is returning to the screen after having been previously paused.
- onStart. Similar to the same call on the activity, this is called when the fragment is about to be placed onscreen.
- onResume. This is called when the fragment is back onscreen.

At this point, your fragment is frolicking on the screen, receiving touch and key events, or just hanging around and looking great. If the user leaves the screen or switches to a view that no longer includes the fragment, the following shutdown lifecycle will take place:

- onPause. This is called if the fragment is removed from the screen or the user presses the home button. This is the only part of the shutdown life-cycle you're guaranteed to get (it would be the only method you get in the rare situation that your application is put in the background and then your process is killed due to resource constraints). onPause is the best time for you to save any data or state information that you want the user to be able to see when the fragment is resumed later.
- onStop. Similar to the activity's version of this method, onStop is called when your fragment has left the screen. It tends to be called in conjunction with the activity's onStop method.
- onDestroyView. This is your last chance to pull data out of the views before they go away.
- onDestroy. This is called when the fragment is being removed from the screen and will not return. This is the time to make sure all your threads are stopped, loaders are canceled, and any broadcast receivers are unregistered.
- onDetach. Called as the fragment loses its association with an activity, onDetach is the last of your methods the system will call before the fragment heads to the great garbage collector in the sky.

### CREATING A FRAGMENT

To create a fragment, you’ll need to make a Java class that extends the Fragment class. An incredibly simple implementation would look something like this:

```
public class ContentFragment extends Fragment{
    @Override
    public View onCreateView(LayoutInflater inflater,
        ViewGroup container, Bundle savedInstanceState) {
        View v = inflater.inflate(R.layout.content_layout, null);
    }
}
```

Fragments, of course, need their own layouts to show anything onscreen. This ContentFragment class will just show a simple text view. Here is the content_layout.xml file whose contents will be drawn as the fragment itself:

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >
    <TextView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/content_text_view"
        />
</LinearLayout>
```

```xml
android:layout_height="match_parent"
android:id="@+id/list_fragment" />
</LinearLayout>
```

This layout can then be set as the content view for a FragmentActivity, like so:

```java
public class ContentViewingActivity extends FragmentActivity{
    public void onCreate(Bundle data){
        super.onCreate(data);
        setContentView(R.layout.content_activity_layout);
    }
}
```

Figure 10.1 shows the results of using XML to make the fragment appear onscreen.

### THE FragmentActivity CLASS

The FragmentActivity is a special class you’ll need to use only if you want to work with fragments on versions of Android earlier than 3.0. For Honeycomb and Ice Cream Sandwich, a simple activity contains all the pieces you need to interact with fragments. You can find the FragmentActivity class in the Android compatibility library.

![](img/47ad0ac10bf11125744ef22c945d3099_242_0.png)

### Fragment example project

Bauhaus commodo store dith American apparel, put a bird on it Austin nostrud eiusmod readymade id aesthetic synth. Portland booth quis polaroid butcher celiac sustainable. Banksy keytar chic, PBR deserunt caries DIY dreamcatcher mustache aesthetic forage. Helvetica keffiyeh laborum biodiesel in dolore. Beard est brunch, viral sartorial twee DIY biodiesel beard artisan shoreditch ut sunt American apparel butcher echo. etsy Terry Richardson American apparel deserunt ullamco synth ethical sed, Portland non tumbler brunch photo booth.

FIGURE 10.1 A fragment with a single text view.
