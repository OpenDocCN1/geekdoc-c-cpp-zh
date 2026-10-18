implementation of <o>AboutView</o> to pass the items in. Replace <o>ContentView</o>() with this:

```
ContentView(items = viewModel.items)
```

Build and run the Android app. It works just like before, but this time it uses a viewmodel.

![](bbox=[0.38157, 0.22569, 0.6175700000000001, 0.58169])

iOS

Open the Xcode project and switch to <o>AboutView.swift</o>.

At the top of the file, make sure to import the <o>shared</o> module by adding this line:

```
import shared
```

Next, inside the <o>AboutView</o> struct, add a property for the viewmodel:

```
@StateObject private var viewModel = AboutViewModel()
```

You annotate the property with <o>@StateObject</o> directive to make SwiftUI create