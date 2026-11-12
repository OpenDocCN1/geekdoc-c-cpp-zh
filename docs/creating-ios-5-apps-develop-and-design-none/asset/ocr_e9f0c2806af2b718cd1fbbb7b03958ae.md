# CLASSES SUPPORTING THE APPLICATION PROXY

Two things must happen before a class can support setting its appearance through an application proxy. First, the class must adopt the UIAppearanceContainer protocol. Next, it must flag the relevant accessors with the UI_APPEARANCE_SELECTOR tag.

A quick search shows that only the following classes currently support the appearance proxy:

+   - UIActivityIndicatorView
+   - UIBarButtonItem
+   - UIBarItem
+   - UINavigationBar
+   - UIProgressView
+   - UISearchBar
+   - UISlider
+   - UISwitch
+   - UISegmentedControl
+   - UITabBar
+   - UITabBarItem
+   - UIToolbar

Unfortunately, the documentation does not clearly label the flagged accessors. However, if you have any questions, you can always open the class's header file. For example, opening UIActivityIndicatorView.h shows that only the color property is properly flagged (OK, you probably could have guessed that from the docs, but still...).

Most notably, UIButton is missing from this list. So, even though iOS 5.0 adds a tintColor property, this property may not do what you want. It won't actually change the color of a rounded rectangle (though, see our custom buttons in the "Rounding Corners with Core Animation" section of Chapter 4). And we cannot simply modify the proxy; we must modify the appearance of each button individually. We'll see this when we create custom buttons using resizable images, coming up next.

```
UIProgressView* proxy =
[UIProgressView appearanceWhenContainedIn:[PopupView class], nil];

proxy.progressTintColor = [UIColor colorWithRed:0.5
                                           green:0.0
                                            blue:0.0
                                           alpha:1.0];

proxy.trackTintColor = [UIColor colorWithRed:0.5
                                       green:0.3
                                        blue:0.3
                                       alpha:1.0];
```