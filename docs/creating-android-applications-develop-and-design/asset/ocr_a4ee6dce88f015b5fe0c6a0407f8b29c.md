# ## SIGNING UP FOR A MAP KEY

Getting a map key is pretty easy. Head over to http://code.google.com/android/maps-api-signup.html and run the command they suggest:

```
```
keytool -list -keystore ~/.android/debug.keystore
```
```

From the sign-up page, you must agree to their terms (which you should probably read first), enter the output from your keytool command, and get your API key. Toss that string into the apiKey section (the highlighted line in the main.xml code) of the MapView, and you're good to go. Remember, the map key is bound to whatever key you signed your .apk with (in this case, the debugging one). When you sign your .apk for release, you'll need to remember to generate a new key for it.

> > **TIP:** If the keytool asks for a password, the default is "android."

# ## RUN, BABY, RUN

You've configured everything, dotted all your i's, and crossed all your t's. It's time to take this map view out for a spin. When it comes time to move and render the map, you'll be primarily interfacing with the MapController, which you'll actually retrieve from the map view itself. The simple work for my example is all done in my sample code's onCreate method:

```
```java
MapView mv;

MapController controller;

@Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        mv = (MapView)findViewById(R.id.map_view);
        controller = mv.getController();
        GeoPoint point = new GeoPoint((int)(40.734641 * 1e6),
                (int)(-73.996181 * 1e6));
        controller.animateTo(point);
        controller.setZoom(12);
    }
```
```

![](bbox=[0.729, 0.276, 0.999, 0.462])