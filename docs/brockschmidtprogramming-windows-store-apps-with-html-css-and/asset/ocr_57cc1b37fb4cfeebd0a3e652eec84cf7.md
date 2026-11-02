```
var singleUse = false;

if (geofenceSingleUse.checked) {
    singleUse = true;
}

// want to listen for enter geofence, exit geofence and remove geofence events
var mask = 0;

mask = mask | Windows.Devices.Geolocation.Geofencing.MonitoredGeofenceStates.entered;
mask = mask | Windows.Devices.Geolocation.Geofencing.MonitoredGeofenceStates.exited;
mask = mask | Windows.Devices.Geolocation.Geofencing.MonitoredGeofenceStates.removed;

var dwellTimeSpan = new Number(parseTimeSpan(dwellTimeField, defaultDwellTimeSeconds));
var durationTimeSpan = null;
if (durationField.value.length) {
    durationTimeSpan = new Number(parseTimeSpan(durationField, 0));
} else {
    durationTimeSpan = new Number(0); // duration required if start time is set
}
var startDateTime = null;
if (startTimeField.value.length) {
    startDateTime = new Date(startTimeField.value);
} else {
    startDateTime = new Date(); // default is 1/1/1601
}

geofence = new Windows.Devices.Geolocation.Geofencing.Geofence(fenceKey, geocircle,
    mask, singleUse, dwellTimeSpan, startDateTime, durationTimeSpan);
} catch (ex) {
    WinJS.log && WinJS.log(ex.toString(), "sample", "error");
}

return geofence;
}
```

What you now do with the Geofence object depends on whether you want foreground or background monitoring. The best way to think about this is that background monitoring should be your default choice. The reasons for this are twofold. First, background monitoring also works when the app is running, thereby allowing you to have just one piece of code to handle monitoring events. Second, if you set up event handlers for the running app alongside a background task, both will pick up geofencing events but the order isn't guaranteed. Thus, you'd choose foreground monitoring only for specific scenarios that would not need background monitoring at all.

Either way, the first step is to add your Geofence object to the GeofenceMonitor (in Windows.Devices.Geolocation.Geofencing), specifically through its geofences vector. To end monitoring of that geofence, just remove that instance from the vector. Be mindful that the GeofenceMonitor is a system object that you access directly (not using new). So, if you have a Geofence in the variable geofence, you start monitoring like so:

```
var monitor = Windows.Devices.Geolocation.Geofencing.GeofenceMonitor.current;
monitor.geofences.push(geofence);
```