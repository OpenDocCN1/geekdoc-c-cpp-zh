
## Xcode

Launch Xcode and open the **iosApp** directory under the starter project for this chapter. You don’t have to select the xcodeproj or the xcworkspace file. Click **Open.**

Once the project is open, you’ll see the two iosApp folders on the left:

On iOS, you would typically use storyboards or create your UI in code if you were developing in UIKit to design your UI. Underneath those storyboards is a complex XML file. While the layout editor in Xcode is nice, it still takes quite a bit of work to design and then hook up to code. SwiftUI is a declarative UI system that’s written entirely in code. No layouts or storyboards. It’s a lot simpler to use and allows a lot of code reuse with smaller views. Xcode provides previews so that you can build small components and view them next to the editor.

# Getting to know SwiftUI

Creating the project using the KMM plugin creates two Swift files: **ContentView.swift** and **iOSApp.swift**. These two files are like a “Hello World” app. They show a text field in the center of the screen with the word “Hello”. The plugin adds several files to make development easier.

# App

Open **iOSApp.swift**:

The starting point in a SwiftUI app is a struct that’s marked with the `@main` attribute above the struct. This struct usually implements the `App` protocol. The `App` protocol requires you to create a variable named `body` that returns a `Scene`. A `Scene` is a container for the root view of a view hierarchy. A `WindowGroup` is a `Scene` and is also a container for your views. On iOS, this will contain only one window, but on macOS and iPadOS, it can contain multiple windows. Since it’s a single expression, a return isn’t required. None of the names of these files are special — the only important piece is to instruct the compiler where to start the app, and you do that with the `@main` tag.

Since `iOSApp` doesn’t describe what your app does, rename the file to `TimezoneApp` by selecting it in the left sidebar and pressing **Return**. Type `TimezoneApp` and press return again. Next, change `struct iOSApp: App` to `struct TimezoneApp: App`.

Next, add the following code before `var body` to change the color of the tab bar

You can also run the app in Android Studio. In Android Studio, make sure iOSApp is selected from the configuration menu:

Then, press the **Run** button:

Open **ContentView.swift**. Delete `Text("Hello")`. Add the following as the first line in the struct:

```
@StateObject private var timezoneItems = TimezoneItems()
```

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

# # Time zone view

Right-click in the iosApp folder and select New File...

Next, select SwiftUI file and click Next:

Then, save as TimezoneView.swift:

Inside the file, first add the import for the shared library:

```swift
import shared
```

Inside of **struct TimezoneView** add the following variables:

```swift
// 1
@EnvironmentObject private var timezoneItems: TimezoneItems
// 2
private var timezoneHelper = TimezoneHelperImpl()
// 3
@State private var currentDate = Date()
// 4
let timer = Timer.publish(every: 1000, on: .main, in: .common).autoconnect()
// 5
@State private var showTimezoneDialog = false
```

+   1. This is the `timezoneItems` object passed in from `ContentView`.
+   2. Create an instance of `timezoneHelper`.
+   3. Get the current date.
+   4. Create a timer to update every second.
+   5. State variable on whether to show the time zone dialog.

`@State` is used with simple struct types, and its state is saved between redraws. Any `@State` property wrapper means the current view owns this data. SwiftUI keeps track of when this `@State` variable changes and redraws the view when its value changes.

`@StateObject` is used with classes. You’ll mostly see `@State` used as SwiftUI views are `struct`s.

Replace `Text("Hello, World")` with the following code:

```swift
// 1
NavigationView {
    // 2
    VStack {
        // 3
        TimeCard(timezone: timezoneHelper.currentTimeZone(),
                 time: DateFormatter.short.string(from: currentDate),
                 date: DateFormatter.long.string(from: currentDate))
        Spacer()
        // TODO: Add List
    } // VStack
    // 4
    .onReceive(timer) { input in
        currentDate = input
    }
    .navigationTitle("World Clocks")
    // TODO: Add toolbar
} // NavigationView
```

+   1. A `NavigationView` allows you to display new screens with a title and will animate the view.
+   2. A `VStack` is a vertical stack. It’s basically the same as a **Column** in JC.
+   3. Call the `TimeCard` class to show the time zone in a nice card format. Use the `short` and `long` `DateFormatter` extensions from the `Utils` class.
+   4. Use your timer. Every time the timer changes, update the date, which will then update the other elements.

If you look at the **Utils.swift** file, you’ll see the definition of the `short` and `long` `DateFormatter` extension fields. Go ahead and run the app. Here’s what it will look like:

# List of time zones

Next, replace `// TODO: Add List` with:

```
```swift
// 1
List {
    // 2
    ForEach(Array(timezoneItems.selectedTimezones), id: \.self) {
        timezone in
        // 3
        NumberTimeCard(timezone: timezone,
                       time: timezoneHelper.getTime(timezoneId:
        timezone),
                       hours: "\(timezoneHelper.hoursFromTimeZone(otherTimeZoneId: timezone)) hours from local",
                       date: timezoneHelper.getDate(timezoneId:
        timezone))
            .withListModifier()
    } // ForEach
    // 4
    .onDelete(perform: deleteItems)
} // List
// 5
.listStyle(.plain)
Spacer()
```

+   1. Create a `List` of items.
+   2. Create an array of selected time zones, and create a card for each one.
+   3. Show the time zone in a nice time card. Use a custom list modifier to remove the row separator and insets. (See **ListModifier.swift**.)
+   4. Add the ability to swipe to delete. You’ll define the `deleteItems` method later.
+   5. Make the list style plain.

The `ForEach` is a special SwiftUI view struct and can be returned as a `View`, unlike a regular `forEach()` function.

Next, `// TODO: Add toolbar` with the following code:

```
```swift
// 1
.toolbar {
    // 2
    ToolbarItem(placement: .navigationBarTrailing) {
        // 3
        Button(action: {
            showTimezoneDialog = true
        }) {
            Image(systemName: "plus")
```
```
