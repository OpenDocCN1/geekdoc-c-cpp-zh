```
```swift
// ...
}
}
}
}
```
```

While you’re in this file, update the `previews` in the `AboutListView_Previews` struct to silence Xcode’s woes.

```
```swift
static var previews: some View {
    AboutListView(
        items: [AboutViewModel.RowItem(title: "Title", subtitle: "Subtitle")],
        footer: "Section Footer"
    )
}
```
```

Next, open **AboutView.swift** and update the usage of `AboutListView` to account for the `footer`.

```
```swift
AboutListView(
    items: viewModel.items,
    footer: "This page was first opened on \(viewModel.firstOpening)"
)
```
```

Build and run the app. Open the **About Device** page by tapping on the **About** button in the bottom toolbar.

![](bbox=[0.392, 0.555, 0.608, 0.847])

Fig. 10.2 - The About page on iOS

# Desktop