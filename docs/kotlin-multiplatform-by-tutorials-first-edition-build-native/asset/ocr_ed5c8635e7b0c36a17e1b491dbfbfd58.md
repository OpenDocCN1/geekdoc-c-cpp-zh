Like `remember` in Jetpack Compose (JC), `StateObject` creates an observable object that’s created once. Each time the view is redrawn, it will reuse the existing object. Other objects can listen for changes, and SwiftUI will update those objects. If you open the **TimezoneItems.swift** file, you’ll see that it’s an `ObservableObject` that **Publishes** a list of time zones and selected time zones. It also asynchronously gets the list of time zones from the `shared` library.

# TabView

`TabView` is the SwiftUI equivalent of Jetpack Compose’s `BottomNavigation`. You can use it to display a tab bar at the bottom of the screen and lets the user switch between different views of the app.

Back in **ContentView.swift**, define `body` as follows:

```
var body: some View {
    // 1
    TabView {
        // 2
        TimezoneView()
            // 3
            .tabItem {
                Label("Time Zones", systemImage: "network")
            }
        // 4
//        FindMeeting()
//            .tabItem {
//                Label("Find Meeting", systemImage: "clock")
//            }
    }
    .accentColor(Color.white)
    // 5
    .environmentObject(timezoneItems)
}
```

+   1. Create a SwiftUI `TabView`.
+   2. The first tab will be the `TimezoneView` that you’ll create next.
+   3. Apply the `tabItem` with a system network icon and the word **Time Zones**.
+   4. The second tab will be the `FindMeeting` view that you haven’t created yet. (It’s commented out for now.)
+   5. Set the `timezoneItems` object as an `environmentObject`.

There are several ways to pass objects around to different views. Here, you pass `timezoneItems` via an Environment Object. The users of this object i.e, any child view, will declare an `@EnvironmentObject` variable that will receive that object.