You can also run the app in Android Studio. In Android Studio, make sure iOSApp is selected from the configuration menu:

![](bbox=[0.325, 0.548, 0.671, 0.631])

Then, press the **Run** button:

![](bbox=[0.287, 0.71, 0.713, 0.746])



Open **ContentView.swift**. Delete `Text("Hello")`. Add the following as the first line in the struct:

```
@StateObject private var timezoneItems = TimezoneItems()
```