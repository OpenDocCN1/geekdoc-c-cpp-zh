

![](img/2f50555a40af4ea8c85f09e577f0c5b9_35_0.png)

你还没有修改 UI，但这可以确保 Gradle 文件仍然可用。

## 查找时间

你是否需要与身处不同时区的同事安排会议？这可能会很麻烦。你想安排的时间他们是否醒着？哪些时间适合安排会议？你将要编写一个 Find Time 应用，帮助找到那些最合适的会议时间。为此，你需要编写一些时区逻辑来确定最佳的会面时间。如果你分别编写 iOS 和 Android 应用，就必须将那套业务逻辑编写两次。

## 业务逻辑

KMP 的主要优点之一是你可以在所有平台之间共享业务逻辑。你将在 shared 模块中编写业务逻辑。该模块是一个多平台模块，你可以将它用于 iOS、Android、桌面端和 Web。

打开 `shared/src` 文件夹，然后打开 `androidMain`、`commonMain` 和 `iosMain` 文件夹。你会找到 `Platform` 和 `Greeting` 类。删除这些类，因为你不会用到它们。请注意，在删除调用它们的代码之前，Android 和 iOS 平台都无法运行。Android Studio 会提示它们被使用的位置。点击 **查看用法**。

![](img/2f50555a40af4ea8c85f09e577f0c5b9_36_0.png)

双击 `return Greeting()` 打开 MainActivity。删除 `greet` 函数、import 语句以及下方对它的引用：

```kotlin
import com.raywenderlich.findtime.Greeting
import android.widget.TextView

fun greet(): String {
    return Greeting().greeting()
}
```

再次执行删除操作，你就能毫无问题地删除这些文件了。

## 日期时间计算

你将使用 JetBrains 的 `kotlinx-datetime` 库来辅助日期时间计算。打开 **shared/build.gradle.kts**，找到 `val commonMain`，将其改为：

```kotlin
val commonMain by getting {
    dependencies {
        // 1
        implementation(Deps.JetBrains.datetime)
        // 2
        implementation(Deps.napier)
    }
}
```

这会导入两个库：

1. JetBrains datetime 库。
2. Napier 日志库。

现在执行 Gradle 同步。

## 日期时间库

Kotlin 的 `kotlinx-datetime` 是一个易于使用的多平台库，可帮助进行基于日期和时间的计算。它使用以下几种数据类型：

- `Instant` 表示某个瞬间。
- `Clock` 模拟真实世界的时钟，并提供当前瞬间。
- `LocalDateTime` 表示带时间的日期，但没有关联的时区。
- `LocalDate` 只表示日期。
- `TimeZone` 和 `ZoneOffset` 帮助你在 `Instant` 和 `LocalDateTime` 之间进行转换。
- `Month` 是一个枚举，表示一年中的所有月份。
- `DayOfWeek` 是一个枚举，表示一周中的所有日子。它使用 `MONDAY`、`TUESDAY` 等值，而不是整数。
- `DateTimePeriod` 表示两个瞬间之间的差异。
- `DatePeriod` 是 `DateTimePeriod` 的子类，表示两个 `LocalDate` 实例之间的差异。
- `DateTimeUnit` 提供一组单位，如 `NANOSECOND`、`WEEK`、`CENTURY` 等，你可以用来对 `Instant` 和 `LocalDate` 执行算术运算。

## 时区辅助类

转到 **shared/commonMain/** 中的 **com/raywenderlich/findtime** 包，创建一个名为 **TimeZoneHelper** 的新 Kotlin 接口。添加以下代码：

```kotlin
interface TimeZoneHelper {
    fun getTimeZoneStrings(): List<String>
    fun currentTime(): String
    fun currentTimeZone(): String
    fun hoursFromTimeZone(otherTimeZoneId: String): Double
    fun getTime(timezoneId: String): String
    fun getDate(timezoneId: String): String
    fun search(startHour: Int, endHour: Int, timezoneStrings: List<String>): List<Int>
}
```

这定义了一个包含七个函数的接口。

- 返回时区字符串列表。（这是来自 JetBrains kotlinx-datetime 库的所有时区列表）
- 返回当前格式化时间。
- 返回当前时区 ID。
- 返回与给定时区相差的小时数。
- 返回给定时区的格式化时间。
- 返回给定时区的格式化日期。
- 搜索一个小时列表，该列表从 `startHour` 开始，到 `endHour` 结束，并且位于所有给定的时区字符串中。

创建接口便于测试。本章不涉及测试，但使用接口可以轻松创建模拟的时区辅助对象。现在，创建该接口的一个实例。右键点击 findtime 文件夹，新建一个名为 **TimeZoneHelperImpl** 的 Kotlin 类。这个类将实现该接口。将这个类改为实现 `TimeZoneHelper`，如下所示：

```kotlin
class TimeZoneHelperImpl: TimeZoneHelper {
}
```

你会看到类下方有一条红色下划线，因为你尚未实现这些方法。将光标保持在 `TimeZoneHelperImpl` 上，按下 **Option-Return**，然后选择 **实现成员**。

![](img/2f50555a40af4ea8c85f09e577f0c5b9_39_0.png)

选择全部并点击 **OK**。你会看到许多 TODO。

从 `getTimeZoneStrings` 开始。这听起来可能很难，但 kotlinx-datetime 库让它变得简单。将 TODO 替换为：

```kotlin
return TimeZone.availableZoneIds.sorted()
```

这一行返回可用的时区 ID 并进行排序。`TimeZone` 会显示为红色。将光标放在 `TimeZone` 上，按 **Option-Return** 导入库。你也可以在接下来的章节中使用这一技巧来导入所需的类。

接下来，你需要一个方法来格式化 datetime 的 `LocalDateTime` 类。在类的底部添加以下方法：

```kotlin
fun formatDateTime(dateTime: LocalDateTime): String {
    // 1
    val stringBuilder = StringBuilder()
    // 2
    var hour = dateTime.hour
    val minute = dateTime.minute
    var amPm = " am"
    // 3
    // For 12
    if (hour > 12) {
        amPm = " pm"
        hour -= 12
    }
    // 4
    stringBuilder.append(hour.toString())
```

该方法接收一个时间范围（如 `8..17`）、要检查的给定小时、用户的当前时区，以及你要对照检查的其他时区。

第一次检查验证该小时是否在时间范围内。如果不在，则无效。

现在，将 `// TODO: Add Current Time` 替换为：

```kotlin
// 1
val currentUTCInstant: Instant = Clock.System.now()
// 2
val currentOtherDateTime: LocalDateTime =
    currentUTCInstant.toLocalDateTime(otherTimeZone)
// 3
val otherDateTimeWithHour = LocalDateTime(
    currentOtherDateTime.year,
    currentOtherDateTime.monthNumber,
    currentOtherDateTime.dayOfMonth,
    hour,
    0,
    0,
    0
)
// TODO: Add Conversions
```

1. 使用 datetime 的 `Clock.System.now` 方法获取 UTC 时区的当前瞬间。
2. 使用 `toLocalDateTime`，传入其他时区，将该瞬间转换为另一个时区。
3. 获取具有给定小时的 `LocalDateTime`。（不需要分钟、秒和纳秒）

现在，将 `// TODO: Add Conversions` 替换为：

```kotlin
// 1
val localInstant = otherDateTimeWithHour.toInstant(currentTimeZone)
// 2
val convertedTime = localInstant.toLocalDateTime(otherTimeZone)
Napier.d("Hour $hour in Time Range ${otherTimeZone.id} is ${convertedTime.hour}")
// 3
return convertedTime.hour in timeRange
```

Napier 是日志库，需要导入。将光标放在 `Napier` 上，按下 **Option-Return** 导入该库。

在上面的代码中，你：

1. 将该小时转换为当前时区。
2. 将你所在时区的小时转换为其他时区。
3. 检查它是否在你的时间范围内。

既然你已经有了 `isValid` 方法，`search` 方法就不会那么难了。你只需要遍历所有给定的时区和小时，检查它们是否有效。将 `search` 方法更新为：

```kotlin
// 1
val goodHours = mutableListOf<Int>()
// 2
val timeRange = IntRange(max(0, startHour), min(23, endHour))
// 3
val currentTimeZone = TimeZone.currentSystemDefault()
// 4
for (hour in timeRange) {
    var isGoodHour = false
    // 5
    for (zone in timezoneStrings) {
        val timezone = TimeZone.of(zone)
        // 6
        if (timezone == currentTimeZone) {
            continue
        }
        // 7
        if (!isValid(
                timeRange = timeRange,
                hour = hour,
                currentTimeZone = currentTimeZone,
                otherTimeZone = timezone
            )
        ) {
            Napier.d("Hour $hour is not valid for time range")
            isGoodHour = false
            break
        } else {
            Napier.d("Hour $hour is valid for time range")
            isGoodHour = true
        }
    }
    // 8
    if (isGoodHour) {
        goodHours.add(hour)
    }
}
// 9
return goodHours
```

在这段代码中，你：

1. 创建一个列表，用于返回所有有效的小时。
2. 创建一个从开始小时到结束小时的时间范围。
3. 获取当前时区。
4. 遍历时间范围内的每个小时。
5. 遍历时区列表中的每个时区。

