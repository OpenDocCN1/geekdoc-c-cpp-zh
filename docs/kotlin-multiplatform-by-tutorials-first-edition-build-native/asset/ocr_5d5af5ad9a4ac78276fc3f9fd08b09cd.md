```
```kotlin
contentDescription = getString(MR.strings.navigation_search)
```
```

Remove the now-unnecessary imports:

```
```kotlin
import androidx.annotation.StringRes
import com.raywenderlich.learn.android.R
```
```

+   - **main/MainBottomBar.kt**: With the previous change, you need to update the `BottomNavigationItem` in the `MainBottomBar`. Replace the `stringResource` call with:

```
```kotlin
text = screen.title,
```
```

And remove its import:

```
```kotlin
import androidx.compose.ui.res.stringResource
```
```

+   - **main/MainTopAppBar.kt**: Replace the `stringResource` call with:

```
```kotlin
text = getString(MR.strings.app_name),
```
```

And remove the imports:

```
```kotlin
import androidx.compose.ui.res.stringResource
import com.raywenderlich.learn.android.R
```
```

+   - **search/SearchContent.kt**: This is the last file that needs to be updated! Scroll down to `AddSearchField` and locate the two calls to `stringResource`. The first one is where you’re defining the `placeholder` and needs to be updated to:

```
```kotlin
text = getString(MR.strings.search_hint),
```
```

The second one is for `leadingIcon`, and you need to change the `description` to:

```
```kotlin
val description = getString(MR.strings.description_search)
```
```

And, as always, remove the imports: