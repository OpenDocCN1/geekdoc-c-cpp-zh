# ### GeoPoints

Google, in its not-so-infinite wisdom, decided that GeoPoints for the map view should not accept latitude and longitude values in degrees like every other API in the SDK. Instead, they take them in 1e6 values. This means, simply, that you must multiply any latitude or longitude value you wish to reference in the map view by 1e6 before handing off. Interesting map errors will result if you forget this step.

# ## WRAPPING UP

In this chapter, I showed you the very basics for finding a device's location and displaying a map onscreen. If you're looking to go further into this topic, you should explore map overlays through the `OverlayItem` class. Overlays let you point out specific locations (addresses, businesses, or cat pictures) to your users.

As always, be very careful what kind of location services you use, especially while the user is not in your application. Nothing will drain a user's battery faster—and make them angrier—than heavy locational lookups in the background. If you're planning a very location-heavy application, be sure to do LOTS of battery-draw testing before you release it. Your users and your application's ratings will be much happier for it.