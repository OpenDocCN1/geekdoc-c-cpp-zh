This function takes a list of current time zones. It’s a `SnapshotStateList` so that this class can change the values, and other functions will be notified of the changes.

+   1. Create an instance of your TimeZoneHelper class.
+   2. Remember the state of the list that will be defined later.
+   3. Create a vertical column that takes up the full width and height.

Replace `// TODO: Add Content` with:

```
```kotlin
// 1
var time by remember { mutableStateOf(timezoneHelper.currentTime())
}
// 2
LaunchedEffect(0) {
    while (true) {
        time = timezoneHelper.currentTime()
        delay(timeMillis) // Every minute
    }
}
// 3
LocalTimeCard(
    city = timezoneHelper.currentTimeZone(),
    time = time, date =
    timezoneHelper.getDate(timezoneHelper.currentTimeZone())
)
Spacer(modifier = Modifier.size(16.dp))

// TODO: Add Timezone items
```
```

+   1. Remember the current time.
+   2. Use Compose’s `LaunchedEffect`. It will be launched once but continue to run. The method will get the updated time every minute. You pass `0` as a parameter to `LaunchedEffect` so that it is not canceled and re-launched when `LaunchedEffect` is recomposed.
+   3. Use the `LocalTimeCard` function you created earlier. Use `TimeZoneHelper`’s methods to get the current time zone and current date.

Return to **MainView**. Replace `// TODO: Replace with screens` with the following:

```
```kotlin
when (selectedIndex.value) {
    0 -> TimeZoneScreen(currentTimezoneStrings)
    // 1 -> FindMeetingScreen(currentTimezoneStrings)
}
```
```

If the index is 0, show the Time Zone screen, otherwise show the Find Meeting