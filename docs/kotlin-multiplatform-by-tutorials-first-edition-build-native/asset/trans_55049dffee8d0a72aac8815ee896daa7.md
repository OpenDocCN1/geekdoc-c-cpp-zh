
search/SearchContent 中，在 AddSearchField 可组合项里，将 `leadingIcon` 中对 `painterResource` 的调用替换为：

```
val icon = icSearch()
```

并删除 import：

```
import androidx.compose.ui.res.painterResource
```

全部完成！再继续几个部分，你的应用 UI 就可以完全共享了。

## 使用自定义字体

两个应用都需要使用 Bitter 字体。之前，你已经将所有文件夹从 `androidApp/res` 移动到了 `commonMain/resources`。打开后，你会看到一组 `bitter_*.ttf`，它们代表你的文本可以使用的字体。

与你在上一节中所做的类似，你需要创建一个 Multiplatform 函数来加载它们。

首先，在 shared-ui 模块的 `commonMain/theme` 中创建一个 `Font.kt` 文件。该类将包含函数声明：

```
@Composable
expect fun Font(name: String, res: String, weight: FontWeight,
style: FontStyle): Font
```

字体可以通过 Android 上的 R 类或桌面上的路径来引用。`res` 参数表示这一点。`weight` 和 `style` 对应其属性，当然，`name` 对应其名称。

打开 `androidMain/theme`，并创建相应的 `Font.kt` 文件，包含以下 actual 实现：

```
@Composable
actual fun Font(name: String, res: String, weight: FontWeight,
style: FontStyle): Font {
    val context = LocalContext.current
    val id = context.resources.getIdentifier(res, "font",
    context.packageName)
    return Font(id, weight, style)
}
```

在使用这些新的排版更新所有 Text 可组合项之前，你需要从 `Type.kt` 中移除对 R 类的引用。打开此文件并删除：

```
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

现在不再有 `BitterFontFamily`，你需要从所有 `fontFamily` 属性中移除这个调用。之后，你需要手动更新所有 Text 样式，因为无法从 Typography 引用你在上面创建的字体。

从 `commonMain/ui` 按字母顺序开始，导航到：

- common/EmptyContent：在 Text 声明中，将 `fontFamily` 参数设置为：

```
fontFamily = Fonts.BitterFontFamily(),
```

- common/EntryContent：在 AddEntryContent 可组合项中，找到四处 Text 用法并添加：

```
fontFamily = Fonts.BitterFontFamily(),
```

- home/HomeContent：滚动到此文件末尾，在 Text 上添加：

```
fontFamily = Fonts.BitterFontFamily(),
```

- home/HomeSheetContent：搜索两处 Text 调用并添加：

```
fontFamily = Fonts.BitterFontFamily(),
```

- latest/LatestContent：在 AddNewPage 和 AddNewPageEntry 的 Text 声明上设置 `fontFamily`：

```
fontFamily = Fonts.BitterFontFamily(),
```

对应的 Resources.kt 文件，内容如下：

```
actual fun getString(resId: StringResource): String {
    return StringDesc.Resource(resId).toString(appContext)
}
```

`appContext` 对应应用程序的 Context，它已在 `PlatformDatabase.kt` 文件中声明，并在 `RWApplication.kt` 中设置。

在 `desktopMain/ui/utils` 中，创建剩余的 `Resources.kt` 文件并添加：

```
actual fun getString(resId: StringResource): String {
    return StringDesc.Resource(resId).localized()
}
```

实现定义完成后，你需要遍历所有类并更新对 R 类的引用。它们将不再访问 `R.string.*`，而是调用你刚刚创建的 `getString` 函数。

从 `commonMain/ui` 按字母顺序开始，导航到：

- bookmark/BookmarkContent：在 BookmarkContent 可组合项中，将 `stringResource` 调用更新为：

```
text = getString(MR.strings.empty_screen_bookmarks)
```

并删除 imports：

```
import androidx.compose.ui.res.stringResource
import com.raywenderlich.learn.android.R
```

- common/EntryContent.kt：找到所有对 `stringResource` 的调用，并按顺序将它们更新为等效的 `getString()`。从顶部开始，将 `description` 值更新为：

```
val description = getString(MR.strings.description_feed_icon)
```

接下来，将引用 `app_ray_wenderlich` 的地方替换为：

```
text = getString(MR.strings.app_ray_wenderlich),
```

最后，将访问 `description_more` 的地方改为：

```
val description = getString(MR.strings.description_more)
```

components/ImagePreview.kt：你只需做一处修改。滚动到 AddImagePreviewEmpty，并将访问 R 类的 `description` 属性更新为：

```
val description = getString(MR.strings.description_preview_error)
```

并删除现在不再使用的 imports：

```
import androidx.compose.ui.res.stringResource
import com.raywenderlich.learn.android.R
```

home/HomeSheetContent.kt：查找对 R 类的访问。第一处是用于决定显示哪个文本的 `if` 条件结果。将此代码块替换为：

```
val text = if (item.value.bookmarked) {
    getString(MR.strings.action_remove_bookmarks)
} else {
    getString(MR.strings.action_add_bookmarks)
}
```

此更新之后，`text` 属性的类型为 String，因此你可以从下面的 Text 可组合项中移除对 `stringResource` 的调用：

```
text = text
```

在文件末尾，还有另一处对 R 的引用。将此调用替换为：

```
text = getString(MR.strings.action_share_link),
```

并删除以下 imports：

```
import androidx.compose.ui.res.stringResource
import com.raywenderlich.learn.android.R
```

latest/LatestContent.kt：在 LatestContent 可组合项中，更新字符串

AddEmptyScreen(getString(MR.strings.empty_screen_loading))

像往常一样，删除不必要的 imports：

```
import androidx.compose.ui.res.stringResource
import com.raywenderlich.learn.android.R
```

main/BottomNavigationScreens.kt：`@StringRes` 是 Android 平台特有的字符串引用。由于你要将这个类与桌面应用共享，你需要将此参数更新为通用类型 — String。将 `stringResId` 改为：

```
val title: String,
```

为此，你需要更新此类中声明的所有对象。

对于 home 对象，分别将 `stringResId` 和 `contentDescription` 更新为：

```
title = getString(MR.strings.navigation_home),
contentDescription = getString(MR.strings.navigation_home)
```

bookmark 对象同理：

```
title = getString(MR.strings.navigation_bookmark),
contentDescription = getString(MR.strings.navigation_bookmark)
```

latest 对象同样：

```
title = getString(MR.strings.navigation_latest),
contentDescription = getString(MR.strings.navigation_latest)
```

最后，对于 search：

```
title = getString(MR.strings.navigation_search),
contentDescription = getString(MR.strings.navigation_search)
```

删除现在不再需要的 imports：

```
import androidx.annotation.StringRes
import com.raywenderlich.learn.android.R
```

main/MainBottomBar.kt：通过之前的更改，你需要更新 MainBottomBar 中的 BottomNavigationItem。将 `stringResource` 调用替换为：

```
text = screen.title,
```

并删除其 import：

```
import androidx.compose.ui.res.stringResource
```

main/MainTopAppBar.kt：将 `stringResource` 调用替换为：

```
text = getString(MR.strings.app_name),
```

并删除 imports：

```
import androidx.compose.ui.res.stringResource
import com.raywenderlich.learn.android.R
```

search/SearchContent.kt：这是最后一个需要更新的文件！滚动到 AddSearchField，找到两处对 `stringResource` 的调用。第一处是你定义 placeholder 的位置，需要更新为：

```
text = getString(MR.strings.search_hint),
```

第二处用于 `leadingIcon`，你需要将 `description` 改为：

```
val description = getString(MR.strings.description_search)
```

而且，像往常一样，删除 imports：
