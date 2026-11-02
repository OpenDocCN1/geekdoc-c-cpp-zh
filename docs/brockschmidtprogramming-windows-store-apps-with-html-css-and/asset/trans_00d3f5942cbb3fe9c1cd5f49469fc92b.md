
- 对于输入元素，监听 `pointerdown`、`pointermove` 和 `pointerup` 事件，这些事件通常你已经需要为显示目的而处理。`eventArgs.currentPoint` 是一个 `Windows.UI.Input.PointerPoint` 对象，包含指针 ID、点坐标以及诸如压力、倾斜和扭转之类的属性。
- 分别将该 `PointerPoint` 对象传递给墨迹管理器的 `processPointerDown`、`processPointerUpdate` 和 `processPointerUp` 方法。
- 在 `processPointerUp` 之后，墨迹管理器会为该路径创建一个 `InkStroke` 对象。然后可以通过墨迹管理器的 `getStrokes` 方法获取这些笔划，并按需渲染。
- 高阶手势也可以直接转换为 `InkStroke` 对象，并通过其 `addStroke` 方法交给管理器。笔划对象也可以使用 `deleteStroke` 删除。

墨迹管理器还提供用于对其包含的笔划执行手写识别、保存和加载数据以及处理绘图和擦除等不同模式的方法。有关完整演示，请查看图 12-9 中所示的 [输入墨迹示例](#)。该示例让你可以看到墨迹功能的全部范围，包括手写识别。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_648_0.png)

**图 12-9** 输入墨迹示例，其应用栏上有许多命令。左上角绿色的“Hello Ink”文本是通过点击识别命令生成的。

SDK 还包含 [输入简化墨迹示例](#)，用于演示更专注的手写识别场景，如图 12-10 所示。你应该知道，这是一个完全不支持触控的应用示例——它严格用于鼠标或手写笔，并且使用按键代替应用栏执行各种命令。查看 simpleink.js 中的 `keydown` 函数可获得 Ctrl+键命令列表；空格键执行对笔划的识别，而退格键则清除画布。如图所示，我认为手写识别效果相当不错！（这说明我在 20 世纪 90 年代初某个时候交给微软工程团队的手写样本一定做出了宝贵贡献。）

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_649_0.png)

图 12-10 输入简化墨迹示例在识别我潦草的基于鼠标的手写方面做得非常好。

## 地理位置

在更广泛地探讨传感器之前，我想单独指出 Windows Store 应用的地理位置功能，因为其 API 与其他传感器结构不同。我们在第 2 章“快速入门”中的 Here My Am! 应用中已经使用过它，但我们需要了解这一非常有用的功能的更完整情况。

与所有其他传感器不同，实际上地理位置是唯一一个必须在清单中声明相关功能的传感器。你在地球上的位置是一种绝对度量，如果可以这样说的话，因此被归类为个人信息。因此，用户必须在应用获取该信息之前给予同意，并且你的应用还必须在 Windows Store 中提供隐私声明。相比之下，其他传感器数据是相对的——例如，你无法真正从设备的倾斜方式、移动方式或照射其上的光线多少来了解一个人的任何信息。因此，你可以在不声明任何特定功能的情况下使用这些其他传感器。

如你所知，地理位置可以通过两种不同的方式获得。当然，主要且最精确的方式是从实际的 GPS 无线电获取读数，该无线电与轨道上数百英里高的地球同步卫星通信。另一种相当有用的方式，尽管并不总是准确，是尝试通过有线网络连接的 IP 地址找到自己的位置，或根据可用 WiFi 热点的位置进行三角定位。不管怎样，WinRT 会尽力为你提供一个不错的读数。

要访问地理位置读数，你必须首先创建 WinRT 地理位置定位器 Windows.Devices.Geolocation.Geolocator 的一个实例。拥有它之后，你就可以调用其 getGeopositionAsync 方法，其结果（传递给你的完成处理程序）是一个 Geoposition 对象（在同一个 Windows.Devices.Geolocation 命名空间中，除非另有说明，这里的一切都是如此）。以下是它在 Here My Am! 中的代码：

```
var locator = new Windows.Devices.Geolocation.Geolocator();

locator.getGeopositionAsync().done(function (position) {
    var position = position.coordinate.point.position;

    //Save for share
    app.sessionState.lastPosition =
        { latitude: position.latitude, longitude: position.longitude };
}
```

getGeopositionAsync 方法还有一个变体，你可以在其中指定两个参数：缓存读数的最大年龄（也就是说，你允许读数有多陈旧）以及你愿意等待响应的超时值。两个值均以毫秒为单位。

一个 Geoposition 包含两个属性：
- coordinate 一个 Geocoordinate 对象，提供 accuracy（米）、altitudeAccuracy（米）、heading（相对于真北的度数）、point（一个包含坐标、海拔和其他详细数据的 Geopoint）、positionSource（来自 PositionSource 的值，标识位置的获取方式，例如 cellular、satellite、WiFi、ipAddress 和 unknown）、satelliteData（一个 GeocoordinateSatelliteData 对象）、speed（米/秒）以及 timestamp（一个 Date）。
- civicAddress 一个 CivicAddress 对象，如果地理位置提供程序提供此类数据，可能包含 city（字符串）、country（字符串，两字母 ISO-3166 国家代码）、postalCode（字符串）、state（字符串）以及 timestamp（Date）属性。92

92 也就是说，civicAddress 属性可能不可用或可能为空。获得它的另一种方式是使用 Bing Maps API，特别是 MapAddress 类，将坐标转换为地址。

你可以通过 Geolocator 的 desiredAccuracy 属性来指示你想要的精度，该属性要么是 PositionAccuracy.default 要么是 PositionAccuracy.high。顺便说一下，后者会消耗更多无线电或网络资源。这可能会在按量计费的宽带连接上产生更高的费用，并缩短电池寿命，因此只有在对用户体验至关重要时才将其设置为 high。你也可以使用 Geolocator.desiredAccuracyInMeters 更具体地指定，它将覆盖 desiredAccuracy。

Geolocator 还提供一个 locationStatus 属性，其值来自 PositionStatus 枚举：ready、initializing、noData、disabled、notInitialized 或 notAvailable。显而易见的是，你无法从处于 ready 状态之外的任何状态的 Geolocator 获取数据。为了跟踪这一点，请监听 Geolocator 的 statuschanged 事件，其中处理程序中的 eventArgs.status 包含新的 `PositionStatus`；当你发现 GPS 设备可能需要几秒钟才能提供读数时，这很有帮助。有关使用此事件的示例，请参阅 Windows SDK 中 [地理位置示例](#) 的 scenario 1（js/scenario1.js）：

```
geolocator = new Windows.Devices.Geolocation.Geolocator();
geolocator.addEventListener("statuschanged", onStatusChanged);  //Remember to remove later

function onStatusChanged(e) {
    switch (e.status) {
    // ...
    }
}
```

`PositionStatus` 和 `statuschanged` 反映了 GPS 设备的就绪状态以及通过设置魅力或通过 PC 设置 > 隐私 > 位置设置的应用程序的位置权限（如果权限被拒绝，状态为 `disabled`）。因此，你可以使用此事件在应用运行时检测权限更改并相应响应。当然，用户在你的应用处于挂起状态时可能在 PC 设置中更改权限，因此你通常还希望在 `resuming` 事件处理程序中检查 Geolocator 状态。

Geolocator 的另外两个有趣的属性是 `movementThreshold`，即设备在触发另一次读数之前可以移动的米数（可用于地理围栏场景），以及 `reportInterval`，即尝试读数之间的毫秒数。对后者要保守设置，将其设置为你真正需要的，因为你再次希望最大限度地减少网络或无线电活动。无论如何，当 Geolocator 进行另一次读数并发现设备已超出 `movementThreshold` 时，它将触发 `positionchanged` 事件，其中 `eventArgs.position` 属性是一个新的 Geoposition 对象。这也在 Geolocation 示例的 scenario 1 中显示（js/scenario2.js）：

```
geolocator.addEventListener("positionchanged", onPositionChanged);

function onPositionChanged(e) {
    var coord = e.position.coordinate;

    document.getElementById("latitude").innerHTML = coord.point.position.latitude;
    document.getElementById("longitude").innerHTML = coord.point.position.longitude;
    document.getElementById("accuracy").innerHTML = coord.accuracy;
}
```

使用 `movementThreshold` 和 `reportInterval` 时，务必根据你使用的与位置相关的数据的精度和/或刷新间隔，认真思考你的应用需要什么。例如，天气数据是区域性的，可能每小时才更新一次。因此，`movementThreshold` 可能会按英里或公里的尺度设置，而 `reportInterval` 为 15、30、60 分钟或更长。另一方面，地图或实时交通应用使用的数据对位置非常敏感，因此阈值会小得多，间隔也会短得多。

出于类似目的，你也可以使用更省电的 *地理围栏* 功能，我们将在下一节讨论。
