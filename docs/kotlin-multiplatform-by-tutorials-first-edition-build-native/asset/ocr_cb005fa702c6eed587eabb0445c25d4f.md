Before updating all the **Text** Composable’s with these new typography, you’ll need to remove the references to the **R** class from **Type.kt**. Open this file and remove:

```
```kotlin
import androidx.compose.ui.text.font.Font
import androidx.compose.ui.text.font.FontFamily
import com.raywenderlich.learn.android.R

private val BitterFontFamily = FontFamily(
    Font(R.font.bitter_bold, FontWeight.Bold),
    Font(R.font.bitter_extrabold, FontWeight.ExtraBold),
    Font(R.font.bitter_light, FontWeight.Light),
    Font(R.font.bitter_regular),
    Font(R.font.bitter_semibold, FontWeight.SemiBold),
)
```
```

Now that there’s no more `BitterFontFamily`, you need to remove this call from all the `fontFamily` properties. Afterward, you need to manually update all the **Text styles**, since it’s not possible to reference the **Fonts** that you’ve created above from **Typography**.

Starting alphabetically on **commonMain/ui**, navigate to:

+   - **common/EmptyContent**: On the `Text` declaration, set the `fontFamily` argument to:

```
```kotlin
fontFamily = Fonts.BitterFontFamily(),
```
```

+   - **common/EntryContent**: On the `AddEntryContent` Composable, look for four `Text` usages and add:

```
```kotlin
fontFamily = Fonts.BitterFontFamily(),
```
```

+   - **home/HomeContent**: Scroll down to the end of this file, and on `Text` add:

```
```kotlin
fontFamily = Fonts.BitterFontFamily(),
```
```

+   - **home/HomeSheetContent**: Search for the two `Text` calls and add:

```
```kotlin
fontFamily = Fonts.BitterFontFamily(),
```
```

+   - **latest/LatestContent**: Set the `fontFamily` on the `Text` declarations on `AddNewPage` and `AddNewPageEntry`:

```
```kotlin
fontFamily = Fonts.BitterFontFamily(),
```
```