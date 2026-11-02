
**提示** 如我们在第 7 章“Collection Controls”中所见，`WinJS.UI.StorageDataSource` 对象简化了为 ListView 控件在各种库上设置文件查询的许多细节。它的 `loadThumbnail` 方法也封装了本节中我们看到的许多细节，帮助你轻松为集合中的项目加载缩略图。更多内容请参阅第 7 章中的“A FlipView Using the Pictures Library”。

## 文件属性

最后但绝对不容忽视的是 `StorageFile.properties` 属性（快说十遍！），以及 `getBasicPropertiesAsync` 方法。轻描淡写地说，这些只是打开各种深入信息的大门中的第一扇，特别是关于文件和媒体文件，如图 11-1 所示，连同其他直接属性和缩略图。可以看出，除了 `StorageFile` 的直接属性外，一些扩展属性是通过 `getBasicPropertiesAsync` 和 `properties` 对象的媒体特定方法检索的。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_580_0.png)

**图 11-1** `StorageFile` 对象与元数据对象之间的关系。

首先，图 11-1 中的所有类都来自 `Windows.Storage.FileProperties` 命名空间（`StorageFile` 本身除外），因此除非另有说明，否则请将其作为我们的上下文。

`BasicProperties` 是我们首先感兴趣的，因为我们在上一节已经看到过缩略图。这是从 `StorageFile.getBasicPropertiesAsync` 获取的内容，它仅提供三个属性：`dateModified` 是最后修改日期，用以补充 `StorageFile.dateCreated`，`size` 是文件的大小，而 `itemDate` 包含系统根据其他属性对文件内容找到的相关日期的最佳尝试。例如，图片或视频的相关日期是拍摄时间，音乐则是发行日期。这实际上非常方便，因为它免除了你自行实现类似启发式的需要，并有助于在应用间保持一致性。

“不过，”你可能会自言自语，“这一切都无聊透顶！一个异步调用只是为了获取一个包含三个属性的对象？”看起来确实如此，直到你看到那个小小的 retrievePropertiesAsync 方法——但让我们稍后再回来，因为它到处都出现（如图 11-1 所示），并且伴随着另一个无处不在的方法 savePropertiesAsync（图中未显示）。

StorageFile.properties 包含一个 StorageItemContentProperties 对象，有趣的是它不包含任何直接属性！它只包含六个方法——其中四个检索媒体特定属性，如下一节所述，在用户媒体库或某些其他任意文件夹上创建画廊体验时特别有帮助。然后另外两个方法就是我们的朋友 retrievePropertiesAsync 和 savePropertiesAsync（通过它们你可以访问与媒体特定方法相同的属性）。

每个 retrievePropertiesAsync 方法都能够检索与文件相关的各种其他元数据的名称-值对数组。你提供的唯一参数是想要的属性名称数组，其中每个名称都是一个字符串，来自 Windows.Properties 的一个非常庞大的列表，例如 System.FileOwner 和 System.FileAttributes。（请注意，许多列出的属性不适用于文件系统实体，如 System.Devices.BatteryLife。）

**提示** 要以字符串形式访问最常见的属性名称，请使用 Windows.Storage.StorageProperties 对象的属性，这在 Visual Studio 中提供自动完成功能的好处。

此示例可在 File access 示例的 scenario 6 中找到，该示例同时使用 getBasicPropertiesAsync 和 retrievePropertiesAsync 来显示基本属性以及最后访问日期和文件所有者（js/scenario6.js，其中 file 为 StorageFile）：

```javascript
var dateAccessedProperty = "System.DateAccessed";
var fileOwnerProperty    = "System.FileOwner";

file.getBasicPropertiesAsync().then(function (basicProperties) {
    outputDiv.innerHTML += "Size: " + basicProperties.size + " bytes<br />";
    outputDiv.innerHTML += "Date modified: " + basicProperties.dateModified + "<br />";

    // Get extra properties
    return file.properties.retrievePropertiesAsync([fileOwnerProperty, dateAccessedProperty]);
}).done(function (extraProperties) {
    var propValue = extraProperties[dateAccessedProperty];
    if (propValue !== null) {
        outputDiv.innerHTML += "Date accessed: " + propValue + "<br />";
    }
    propValue = extraProperties[fileOwnerProperty];
    if (propValue !== null) {
        outputDiv.innerHTML += "File owner: " + propValue;
    }
});
```

`retrievePropertiesAsync` 的结果，在上面的代码中的 `extraProperties` 变量中，是一个简单的 `Map` 集合。我们在第 6 章“Maps and Property Sets”一节中见过 map。关于 map 的一个关键点是，你可以使用 `[]` 运算符访问其成员，如上所示，但 map 不是数组，也不具有数组方法。如果你想遍历 map，最好的方法是将其传递给 `Object.keys` 并循环该数组。例如，上面的特定查找代码可以用以下内容替换：

```
Object.keys(extraProperties).forEach(function (key) {
    outputDiv.innerHTML += key + ": " + extraProperties[key] + "<br/>";
});
```

当然，你可以使用单独的 map 对象来查找 `key` 中属性名称的 UI 标签。

**注意** 如果请求的属性在文件上不可用，`retrievePropertiesAsync` 将不会在 map 中为其包含条目，但 map 的 `size` 属性仍将反映原始输入数组的大小。因此，使用 `Object.keys(<map>).length` 来确定实际返回的属性数量。

这非常有用之处在于，来自 `retrievePropertiesAsync` 的 map 直接连接到底层文件的属性存储。这意味着你可以修改其内容并添加新条目，调用 `savePropertiesAsync`（不带参数），瞧！你刚刚更新了文件上的这些属性。当然，这假设这些属性对所讨论的文件类型是可写的并且受支持。如果它们受支持但为只读，根据我的经验，`savePropertiesAsync` 将会忽略它们。另一方面，如果它们不受支持，该方法将抛出一个消息为“The parameter is incorrect.”的异常。

例如，File access 示例中创建的 sample.dat 文件不支持任何可写属性，因此不是一个好的测试用例。如果你改用图像文件（如 JPEG），你可以写入诸如 `System.Keywords` 或 `System.Author` 之类的属性。（检查什么可写的一个好方法是右键单击 Windows 资源管理器中某类型的文件，选择属性，然后查看详细信息选项卡，以查看哪些属性可以编辑，哪些显示为只读。）

为了展示一点代码，假设这里的 `file` 指向一个 JPEG，`extraProperties` 来自一个 `retrievePropertiesAsync` 调用，并且我们想要添加一些关键字：

```
extraProperties.insert("System.Keywords", "sample keyword");
file.properties.savePropertiesAsync().done(function () {
    console.log("success");
});
```

如果我们在 `extraProperties` 中做了任何其他更改，那些也会被保存。或者，我们可以向 `savePropertiesAsync` 传递一个 `Windows.Foundation.Collections.PropertySet` 对象，其中包含我们想要设置的具体属性，在本例中为 `System.Author`：

```
var propsToAdd = new Windows.Foundation.Collections.PropertySet()
propsToAdd.insert("System.Author", currentAuthor);
```

```
    file.properties.savePropertiesAsync(propsToAdd).done(function () {
        console.log("success");
    });
```

我们将在下一节中看到一个更完整的示例，其中包含图像文件和 ImageProperties 对象。

**提示** 避免在另一个保存仍未完成时调用 savePropertiesAsync，例如在第一个尚未完成时运行上面的第二个代码片段。这样做将抛出消息为"A method was called at an unexpected time."的异常。相反，将属性更改合并为一次调用，或使用 promise 链按顺序运行异步操作。

### 媒体特定属性

在 Windows.Storage.FileProperties 中的 BasicProperties 类旁边，我们还有 StorageFile.properties.get*PropertiesAsync 方法返回的那些：ImageProperties、VideoProperties、MusicProperties 和 DocumentProperties。尽管我们不得不深入挖掘才能找到这些，但它们各自包含更深的信息宝库——我的意思是真的很深！下面的表格依次总结了这些，每个对象都包含 retrievePropertiesAsync 和 savePropertiesAsync 方法，如我们所见，以便你可以处理在媒体特定对象中未直接公开的额外属性。

请注意，表格顶部的链接标识了最相关的 Windows 属性组。

**ImageProperties**：来自 StorageFile.properties.getImagePropertiesAsync  
**附加属性**：System.Image, System.Photo, System.Media

| 属性 | 数据类型 | 适用的 Windows 属性 |
| --- | --- | --- |
| Title | String | System.Title |
| dateTaken | Date | System.Photo.DateTaken |
| latitude | Double (see below) | System.GPS.LatitudeDecimal, or combination of System.GPS.Latitude, System.GPS.LatitudeDenominator, System.GPS.LatitudeNumerator, and System.GPS.LatitudeRef |
| longitude | Double (see below) | System.GPS.LongitudeDecimal, or combination of System.GPS.Longitude, System.GPS.LongitudeDenominator, System.GPS.LongitudeNumerator, and System.GPS.LongitudeRef |
| cameraManufacturer | String | System.Photo.CameraManufacturer |
| cameraModel | String | System.Photo.CameraModel |
| width | Number in pixels | System.Image.HorizontalSize |
| height | Number in pixels | System.Image.VerticalSize |
| orientation | A FileProperties.PhotoOrientation object containing unspecified, normal, flipHorizontal, flipVertical, transpose, transverse, rotate90, rotate180, rotate270 | System.Photo.Orientation |
| peopleNames | String vector | System.Photo.PeopleNames |
| keywords | String vector | System.Keywords |
| rating | Number (1-99 with 0 meaning “no rating”) | System.Rating |
