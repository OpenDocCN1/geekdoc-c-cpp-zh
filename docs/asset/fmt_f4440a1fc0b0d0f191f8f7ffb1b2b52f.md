
这产生了以下可用标签列表。注意这不是数据，只是 EXIF 标签列表：(256, `.ImageWidth`), (257, `.ImageLength`), (258, `.BitPerSample`), (259, `.Compression`), (262, `.PhotometricInterpretation`), (270, `.ImageDescription`), (271, `.Make`), (272, `.Model`), (273, `.StripOffsets`), (274, `.Orientation`), (277, `.SamplesPixel`), (278, `.RowsPerStrip`), (279, `.StripCounts`), (282, `.Resolution`), (283, `.Resolution`), (284, `.PlanarConfiguration`), (296, `.Resolution`), (301, `.TransferFunction`), (305, `.Soft`), (306, `.DateTime`), (315, `.Artist`), (318, `.WhitePoint`), (319, `.PrimaryChromaticity`), (321, `.BitsPerComponent`), (324, `.JPEGCount`), (329, `.YCCOOffset`), (330, `.SubSampling`), (331, `.YCCPosition`), (332, `.ReferenceWhite`), (3407, `.FromFile`), (3421, `.RelatedImageWidth`), (3422, `.CFApparent`), (3423, `.CFPattern`), (3432, `.BrightnessValue`), (3433, `.Copyright`), (3434, `.ExposureTime`), (3437, `.FNumber`), (3465, `.EXIFOffset`), (3472, `.InterColorProfile`), (3480, `.ExposureProgram`), (3482, `.Sensitivity`), (3483, `.GPSInfo`), (3485, `.TimeZoneOffset`), (3486, `.Noise`), (3487, `.Interface`), (3488, `.GPSResponse`), (3683, `.IFDOffset`), (3685, `.Flash`), (3686, `.DateTimeOriginal`), (3688, `.DateTimeDigitified`), (3721, `.ComponentsConfiguration`), (3732, `.CompressedBitsPerPixel`), (3737, `.ApertureValue`), (3738, `.BrightnessValue`), (3730, `.ExposureBias`), (3731, `.ExposureValue`), (3732, `.SubjectDistance`), (3733, `.MeteringMode`), (3734, `.LightSource`), (3735, `.Flash`), (3736, `.FocalLength`), (3737, `.FlashEnergy`), (3738, `.SpatialFrequencyResponse`), (3739, `.Noise`), (3740, `.ImageNumber`), (3794, `.SecClassification`), (3795, `.ImageHistory`), (3796, `.SubjectLocation`), (3797, `.Owner`), (3798, `.TIFFDirectoryStandard`), (3750, `.MakerNote`), (3751, `.UserComment`), (3752, `.SubTime`), (3753, `.SubTimeOriginal`), (3752, `.SubjectDigitified`), (4091, `.FlashPixVersion`), (4096, `.ColorScheme`), (4092, `.EXIFImageWidth`), (4093, `.EXIFImage`), (4094, `.RelatedSource`), (4146, `.EXIFInteroperabilityOffset`), (4148, `.Flash`), (4149, `.SpatialFrequencyResponse`), (4186, `.PlaneXResolution`), (4187, `.HostPlanResolution`), (4188, `.HostPlanResolutionUnit`), (4192, `.SubjectLocation`), (4193, `.ExposureIndex`), (4195, `.SensingMethod`), (4128, `.FileSource`), (4129, `.SceneType`), (4130, `.CFApplication`)

时间是一种计数，允许社会以普通方式运行，使所有方都能轻松理解时间表示并对事件顺序达成一致。自 1972 年以来，各国的国际标准是协调世界时（UTC）。UTC 是全球各国官方时间的基础；它由世界通过的一项民主条约管理，该条约指定国家计量机构（NMIs）作为 UTC 时间源。美国国家标准技术研究院（NIST）和英国国家物理实验室（NPL）是 NMI 的两个例子。大约有 50 个计量中心负责官方时间；在检查数字设备时，时区起着关键作用；它们根据计算机的时间提供事件和动作的定位。

## 引言

设置。例如，如果计算机的时间被设置为纽约，则本地时间比 UTC 慢 5 小时（落后 5 小时）。最后，美国许多州和外国国家实行夏令时，大多数现代操作系统会自动调整这种观测，这会导致在与 UTC 比较时或在尝试跨时区同步事件时产生额外的差异和计算。

在打印的文本中，我突出显示了直接感兴趣的 TAGS，包括 `GPSInfo`、`TimeZoneOffset` 和 `DateTimeOriginal`。

需要注意的是，不能保证这些 TAGS 在每张图像中都是可用的；相反，它们是图像中可能存在的一组广泛的键值对。每个制造商都会独立决定将包含哪些值。你必须对每张图像的键值对进行处理，以确定哪些 TAGS 实际上是可用的。我将向你展示如何操作。

当你扫描此列表时，你可能会发现其他对你的调查活动感兴趣的 TAGS，你可以对这些值使用此处定义的相同方法。

## 确定可用的 EXIF GPSTAGS

接下来，我想深入研究一下 `GPSInfo` TAG，因为我们本章的目标是提取特定图像的基于 GPS 的位置数据。我通过编写以下几行代码，采用类似的方法来确定下一级可用的 GPSTAGS。

### 代码脚本 5.7 提取 GPSTAG TAGS

```python
>>> PIL.EXIFtags GPSTAGS
>>> gps = GPSTAGS.items(self)
>>> gps.sort()
>>> print(gps)
```

```
[0., 'GPSVersionID'), (1, 'GPSLatitudeRef'), (2, 'GPSLatitude'),
(3, 'LongitudeRef'), (4, 'Longitude'), (5, 'GPSAltitudeRef'),
(6, 'GPSAltitude'), (7, 'GPSInstName'), (8, 'GPSSatellites'), (9, 'GPSStatus'),
(10, 'GPSMeasureMode'), (11, 'GPSDOOP'), (12, 'GPSSpeedRef'), (13, 'GPSSpeed'),
(14, 'GPSTrack'), (15, 'GPSTrack'), (16, 'GPSImgDirectionRef'), (17,
GPSImgDirection), (18, 'GPSDatum'), (19, 'GPSDestLatitudeRef'), (20,
GPSDestLatitude), (21, 'GPSDestLongitudeRef'), (22, 'GPSBestLongitude'),
(23, 'GPSDestBearingRef'), (24, 'GPSDestBearing'), (25,
GPSDestDistanceRef), (26, 'GPSDestDistance')]
```

我已经识别了一些我们为了确定照片位置和时间所需的 GPSTAGS。需要指出的是，无法保证主体图像中会有任何或所有这些标签。

# 第 5 章 电子取证提取（JPEG 和 TIFF）

经度和纬度位置提供了精确定位地球上某个特定位置的能力。全球定位系统和内置智能手机和相机中的 GPS 接收器可以以经纬度坐标的形式提供非常准确的地理位置信息。如果经过配置，当事件发生时，这些地理位置信息可以直接嵌入照片、电影和其他数字对象中。从数字对象中提取地理位置信息，然后将这些数据输入 Mapquest、Google Earth 等在线服务，可以提供该数字对象何地以及何时创建的证据。

如果我们想利用 TAGS 来确定位置，我们需要对感兴趣的 TAGS 及其含义和用法有更好的定义和理解。

- `GPSLatitudeRef`: 纬度由赤道以北或以南的度数指定。不在赤道范围内的点在 0 到 90 度之间。这些点的引用值被用于定义纬度相对于赤道的位置。由于该值在 EXIF 中是以正整数形式指定的，如果纬度参考（Latitude Reference）为“S”或南，则必须将整数值转换为负值。
- `GPSLatitude`: 表示以度为单位的纬度。EXIF 数据指定这些整数度，随后是分，然后是秒。
- `GPSLongitudeRef`: 经度由主午子线以东或以西的度数指定。基于通过英国格林维治皇家天文台的主午子线，该线被定义为经度零度。主午子线以西的点范围从 0 到 –180 度。主午子线以东的点范围从 0 到 180 度。此引用值被用于定义经度相对于格林维治的位置。由于该值在 EXIF 中是以正整数形式指定的，如果经度参考（Longitude Reference）为西或“W”，
- `GPSLongitude`: 表示以度为单位测量的经度。EXIF 数据指定这些整数度，随后是分，然后是秒。
- `GPSTimeStamp`: 指定拍摄照片时的世界协调时间（Universal Coordinated Time）。

由于 EXIF 结构包含的数据是数字值，它们容易受到操纵和伪造。因此，保护图像或直接从智能移动设备获取它们使得欺诈性修改的可能性降低，且更难实现。

现在我们已经对照片中可能提供的 TAGS 有了基本的了解，让我们来看一张真实的照片。图 5.4 描述了一张从互联网下载的图像，并将作为本次实验的对象。

| Tag | Value |
| :--- | :--- |
| 271 | (Canon) |
| 272 | (Canon) |
| 282 | (300, 1) |
| 283 | (300, 1) |
| 296 | 2008-08-05 23:48:04 |
| 306 | unknown |
| 315 | E |
| 33432 | solar.com |
| 33434 | (1, 100) |
| 33437 | (22, 101) |
| 34665 | 440 |
| 34850 | 2 |
| 34853 | (0, 2, 0) |
| 1 | N |
| 55 | 1 |
| 55 | 1 |
| 37417 | 1285 |
| 3 | E |
| 10 | (41, 1) |
| 55 | 1 |
| 5324 | 1253 |
| 5 | 0 |
| 6 | 1 |
| 36848 | 400 |
| 36851 | 400 |
| 36868 | 2008-08-05 23:48:04 |
| 37378 | 2008-08-05 23:48:04 |
| 37381 | 2008-08-05 23:48:04 |
| 37383 | 2008-08-05 23:48:04 |
| 37385 | 2008-08-05 23:48:04 |
| 41486 | 2008-08-05 23:48:04 |
| 41487 | 2008-08-05 23:48:04 |
| 41488 | 2008-08-05 23:48:04 |
| 41489 | 2008-08-05 23:48:04 |
| 41490 | 2008-08-05 23:48:04 |

# 第 5 章 取证法证提取（JPEG 和 TIFF）

![](img/77956026d6b06352c72ae6ac437ce8ab_151_0.png)

图 5.5

从 Cat.jpg 中提取的 GPS 坐标映射。

# 代码解析 139

| 表格 5.1 GPS/EXIF 提取的基本要求 |
| 要求编号 | 要求名称 | 简要描述 |
| --- | --- | --- |
| GPS-001 | 命令行参数 | 允许用户指定包含示例图像的目录，以尝试从中提取 GPS 信息 |
| GPS-002 | 日志 | 程序必须生成一份法证审计日志 |
| GPS-003 | 输出 | 程序应根据找到的 GPS 信息生成纬度和经度值列表。格式必须简单，纬度值顺序排列，以便粘贴到在线地图应用中 |
| GPS-004 | 错误处理 | 应用程序必须支持对所有执行的操作进行错误处理和记录。这将包括文本描述和时间戳 |

| 表格 5.2 设计考虑与库映射 |
| 要求 | 设计考虑 | 库选择 |
| --- | --- | --- |
| 用户输入 (001) | 关键字和目标文件的用户输入 | 我将使用标准库模块中的 `argparse` 来获取用户输入 |
| 输出 (003) | 提取的 GPS 位置将使用简单的内置命令打印 | 我将使用 Python Image Library 和标准 Python 语言来提取并格式化输出，以便直接复制粘贴到网页：http://www.clarinet.com/lat/ |
| （附加） | 提取额外的 EXIF 和 GPS 值，并将遇到的每个文件的记录数据记录在 CSV 文件中 | 使用 Python Image Library 和 Python CVS Library |
| (002 和 004) 日志和错误处理 | 在处理文件和 EXIF 数据过程中可能会发生错误。因此，对这些潜在错误的处理必须是严密的 | Python 标准库包含一个日志设施，我可以利用它来报告处理过程中发生的任何事件或错误。对于此应用程序，我将创建一个重用的日志类 |

# 第 5 章 取证法证提取（JPEG 和 TIFF）

![](img/77956026d6b06352c72ae6ac437ce8ab_153_0.png)

**图 5.6**

p-gpsExtractor 上文图。

![](img/77956026d6b06352c72ae6ac437ce8ab_153_1.png)

**图 5.7**

WingIDE 项目概述。

### 主程序

`p-gps.py`: 这是该应用程序的主程序，处理整个程序流以及处理用户通过命令行指定的文件夹中包含的每个潜在图像文件。Main 将数据写入标准输出，以便于将数据复制粘贴到网页中进行地图查看。Main 处理到 CSV 文件的输出，提供每个处理文件的结果，以及任何法证日志条目。

# 日志类

`Logging.py`: 新的 `logger` 类在 Python 类中抽象了日志函数，用于处理法证日志功能。这将允许未来的应用程序将日志传递给任何模块或函数，从而消除对全局变量的需求。

### csv 处理器

`csvHandler.py`: 这个用于处理创建和写入 CSV 文件的修改类提供了一个写入 CSV 格式输出文件的单点接口，再次是为了抽象函数并使接口更简单。未来将对该类进行更多工作以进一步实现抽象化。

### 命令行解析器

`commandParser.py`: 我将 `commandParser.py` 分离到单独的文件，以便此应用程序及未来应用程序具有更好的移植性。这允许主行解析器被处理、修改或增强，并且与主程序的耦合更松。与日志函数一样，这最终将被转换为基于类的模块，以允许跨模块访问。

# EXIF 和 GPS 处理器

`_modEXIF.py`: 此模块直接与 PIL 接口，从包含 EXIF 数据的图像文件中提取所需的 EXIF 和 GPS 数据。

# 查看代码

### 主程序

```python
# GPS 提取
# Python法证
# 不需要 HASP
#
```

```python
import os
import _modEXIF
import _csvHandler
import _commandParser
from Logging import ForensicLog
```

对于主过程，我们需要导入 `os` 来处理文件夹、命令行处理、`csvHandler` 以及新的 `ForensicLog` 类。

# 处理命令行

`userArgs = _commandParser.CommandLine()`

通常我处理命令行参数以获取用户指定的值。如果解析成功，我们创建一个新的日志对象来处理必要的事件并写入第一个日志。

```python
# 创建日志
logPath = userArgs.logPath+"ForensicLog.txt"
log = ForensicLog(logPath)
log.writeLog("INFO", "开始扫描")
```

接下来我创建一个 CSV 对象，我将使用它将数据写入包含文件的 CSV 结果。

```python
csvPath = userArgs.csvPath+"ImageResults.csv"
csv=_csvHandler.CSVWriter(csvPath)
```

为了获取 GPS 提取的用户指定的目录，尝试打开并处理目录中的每个文件。如果发生任何错误，将使用 `try-except` 捕获并将相应的错误写入法证日志。
