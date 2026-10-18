and hold an instance of `AboutViewModel` for the lifetime of `AboutView`.

You’ll get a compiler error telling you that `AboutViewModel` should conform to `ObservableObject` protocol so that you could annotate it with `@StateObject`. Don’t worry — it’s pretty easy to fix. Add the conformance to this protocol by adding this block to the end of the file:

```
```swift
extension AboutViewModel: ObservableObject {
}
```
```

> **Note:** In Swift, you can conform to protocols anywhere. Contrary to Kotlin, you don’t need to do it when defining the type.

Next, open **AboutListView.swift**. Remove the `RowItem` struct as well as the `items` property. Then, add a property to hold the items this view shows as follows:

```
```swift
let items: [AboutViewModel.RowItem]
```
```

Don’t forget to import the `shared` module.

Inside the `AboutListView_Previews` struct, change `AboutListView()` invocation to the following:

```
```swift
AboutListView(items: [AboutViewModel.RowItem(title: "Title",
subtitle: "Subtitle")])
```
```

In the code above, you are using a hardcoded row item to fix the UI preview inside Xcode.

Go back to **AboutView.swift** and pass the needed parameter to `AboutListView`:

```
```swift
AboutListView(items: viewModel.items)
```
```

Build and run to see the result of refactoring you just did.