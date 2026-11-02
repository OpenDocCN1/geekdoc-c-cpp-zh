![](bbox=[0.22, 0.11, 0.55, 0.29])

# Running Offline

The other user experience that is likely to earn your app a better reputation is how it behaves when there is no connectivity or when there’s a change in connectivity. Ask yourself the following questions:

+   - What happens if your app starts without connectivity, both from tiles (primary and secondary) and through contracts such as search, share, and the file picker?
+   - What happens if your app runs the first time without connectivity?
+   - What happens if connectivity is lost while the app is running?
+   - What happens when connectivity comes back?

As described above in the “Connectivity Awareness” section, use the networkstatuschanged event to handle these situations while running and your resuming handler to check if connection status changed while the app was suspended. If you have a background task for to the networkStateChange trigger, it would primarily save state that your resuming handler would then check.

It’s perfectly understood that some apps just can’t run without connectivity, in which case it’s appropriate to inform the user of that situation when the app is launched or when connectivity is lost while the app is running. In other situations, an app might be partially usable, in which case you should inform the user more on a case-by-case basis, allowing them to use unaffected parts of the app. Better still is to cache data that might make the app even more useful when connectivity is lost. Such data might even be built into the app package so that it’s always available on first launch.

Consider the case of an ebook reader app that would generally acquire new titles from an online catalog. For offline use it would do well to cache copies of the user’s titles locally, rather than rely solely on having a good internet connection (subject to data transfer limits and appropriate user consent, of course). The app’s publisher might also include a number of popular free titles directly in the app package such that a user could install the app while waiting to board a plane and have at least those books ready to go when the app is first launched at 30,000 feet. Other apps might include some set of preinstalled data at first and then add to that data over time (perhaps through in-app purchases) when unrestricted networks are available. By following network costs closely, such an app might defer downloading a large data set until either the user confirms the action or a different connection is available.