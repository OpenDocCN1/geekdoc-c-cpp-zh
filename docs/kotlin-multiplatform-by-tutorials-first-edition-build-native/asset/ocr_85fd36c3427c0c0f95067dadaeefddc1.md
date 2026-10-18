Now that you have your cards ready, it’s time to put them all together in one screen. In the ui directory, create a new file named TimeZoneScreen.kt. Add the imports and a constant:

```
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.*
import androidx.compose.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.lazy.items
import androidx.compose.material.Icon
import androidx.compose.material.Icon
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Delete
import androidx.compose.runtime.*
import androidx.compose.runtime.snapshots.SnapshotStateList
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
dependencies.com.raywenderlich.findtime.TimeZoneHelper
import com.raywenderlich.findtime.TimeZoneHelperImpl
import kotlinx.coroutines.delay
const val timeMillis = 1000 * 60L // 1 second
```

Next, create the composable:

```
@Composable
fun TimeZoneScreen(
    currentTimezoneStrings: SnapshotStateList<String>
) {
    // 1
    val timezoneHelper: TimeZoneHelper = TimeZoneHelperImpl()
    // 2
    val listState = rememberLazyListState()
    // 3
    Column(
    modifier = Modifier
        .fillMaxSize()
    ) {
    // TODO: Add Content
    }
}
```