```
}
) {
    // 4
    Icon(
        imageVector = Icons.Default.Add,
        contentDescription = null
    )
}
```

+   1. For the first page, create a `FloatingActionButton`.
+   2. Use Compose’s `Modifier` function to add padding.
+   3. Set a click listener. Set the variable to show the add dialog screen. Changing this value will cause a redraw of the screen.
+   4. Use the `Add` icon for the FAB.

# Bottom navigation

Compose has a `BottomNavigation` function that creates a bottom bar with icons. Underneath, it’s a Compose `Row` class that you fill with your content. Replace `// TODO: Add bottom bar` with:

```
// 1
BottomNavigation {
    // 2
    bottomNavigationItems.forEachIndexed { i, bottomNavigationItem ->
        // 3
        BottomNavigationItem(
            // 4
            icon = {
                Icon(
                    bottomNavigationItem.icon,
                    contentDescription =
                        bottomNavigationItem.iconContentDescription
                )
            },
            // 5
            selected = selectedIndex.value == i,
            // 6
            onClick = {
                selectedIndex.value = i
            }
        )
    }
}
```

+   1. Create a `BottomNavigation` composable.
+   2. Use `forEachIndexed` to go through each item in your list of navigation items.
+   3. Create a new `BottomNavigationItem`.