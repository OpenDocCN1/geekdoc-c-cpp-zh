call to:

```
```kotlin
AddEmptyScreen(getString(MR.strings.empty_screen_loading))
```
```

As always, remove the unnecessary imports:

```
```kotlin
import androidx.compose.ui.res.stringResource
import com.raywenderlich.learn.android.R
```
```

+   - **main/BottomNavigationScreens.kt:** `@StringRes` is a string reference specific to the Android platform. Since you’re sharing this class with a desktop app, you need to update this parameter to a common type — **String**. Change `stringResId` to:

```
```kotlin
val title: String,
```
```

With that, you need to update all the objects declared in this class.

For the `home` object, update the `stringResId` and the `contentDescription`, respectively to:

```
```kotlin
title = getString(MR.strings.navigation_home),
```
```

```
```kotlin
contentDescription = getString(MR.strings.navigation_home)
```
```

The same applies to the `bookmark` object:

```
```kotlin
title = getString(MR.strings.navigation_bookmark),
```
```

```
```kotlin
contentDescription = getString(MR.strings.navigation_bookmark)
```
```

And to `latest`:

```
```kotlin
title = getString(MR.strings.navigation_latest),
```
```

```
```kotlin
contentDescription = getString(MR.strings.navigation_latest)
```
```

Finally, for `search`:

```
```kotlin
title = getString(MR.strings.navigation_search),
```
```