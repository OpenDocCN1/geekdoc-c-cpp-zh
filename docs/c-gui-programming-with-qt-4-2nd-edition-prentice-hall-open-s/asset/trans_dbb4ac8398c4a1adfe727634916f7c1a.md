

```cpp
CursorHandler::currentImageNumber() const
{
    return currentImageNo;
}
```

这个简单的函数返回设备文件指针当前所在位置的光标编号。

一旦构造了处理程序，用户就可以以任何顺序调用它的任何一个公共函数。这是一个潜在的问题，因为我们必须假设只能进行串行读取，并且在执行任何其他操作之前，我们需要先读取文件头。我们通过在那些依赖于文件头已读取的函数中调用 `readHeaderIfNecessary()` 函数来解决这个问题。

```cpp
int CursorHandler::imageCount() const
{
    readHeaderIfNecessary();
    return numImages;
}
```

此函数返回文件中的图像数量。对于一个没有发生错误的有效文件，它将返回至少为 1 的计数值。

下一个函数相当复杂，因此我们将分部分进行复习：

```cpp
bool CursorHandler::read(QImage *image)
{
    readHeaderIfNecessary();

    if (state != BeforeImage)
        return false;
}
```

`read()` 函数读取从当前设备指针位置开始的任意图像的数据。如果文件头读取成功，或者在读取了一幅图像后设备指针位于另一幅图像的开头，我们就可以读取下一幅图像。

```cpp
quint32 size;
quint32 width;
quint32 height;
quint16 numPlanes;
quint16 bitsPerPixel;
quint32 *compression;
```

```cpp
QDataStream in(device());
in.setByteOrder(QDataStream::LittleEndian);
in >> size;
if (size != 40) {
    enterErrorState();
    return false;
}
in >> width >> height >> numPlanes >> bitsPerPixel >> compression;
height /= 2;

if (numPlanes != 1 || bitsPerPixel != 1 || compression != 0) {
    enterErrorState();
    return false;
}

in.skipRawData((size - 20) + 8);
```

我们创建了一个 `QDataStream` 来读取设备。我们必须设置字节序以匹配 `.cur` 文件规范指定的格式。不需要设置 `QDataStream` 版本号，因为整数和浮点数的格式在不同的数据流版本之间并没有变化。接下来，我们读取光标头数据的各项内容，并使用 `QDataStream::skipRawData()` 跳过头数据中的无关部分以及 8 字节颜色表。

我们必须考虑到所有的特殊性——例如，将高度减半，因为 `.cur` 文件提供的高度是图像高度的两倍。在单色 `.cur` 文件中，`bitsPerPixel` 和 `compression` 值始终为 1 和 0。如果遇到任何问题，我们就调用 `enterErrorState()` 并返回 `false`。

```cpp
QByteArray xorBitmap = readbitmap(width, height, in);
QByteArray andBitmap = readbitmap(width, height, in);

if (in.status() != QDataStream::Ok) {
    enterErrorState();
    return false;
}
```

文件中的后续项是两个位图，一个是 XOR 掩码，另一个是 AND 掩码。我们将它们读入 `QBitArray` 而不是 `QBitmap`。`QBitmap` 是一个设计用于在屏幕上进行绘制和绘画的类，但我们在这里需要的是一个纯位位数组。

我们完成了文件的读取，检查 `QDataStream` 的状态。在错误状态下，它将保持在该状态并只能返回零。例如，如果读取第一个位数组时失败，尝试读取第二个位数组将导致一个空的 `QBitArray`。

```cpp
*image = QImage(width, height, QImage::Format_ARGB32);
```

```cpp
for (int i = 0; i < int(height); ++i) {
    for (int j = 0; j < int(width); ++j) {
        QRgb color;
        int bit = (i * width) + j;

        if (andbit.testBit(bit)) {
            if (xorBitmap.testBit(bit)) {
                color = 0x7F7F7F7F;
            } else {
                color = 0x00FFFFFF;
            }
        } else {
            if (xorBitmap.testBit(bit)) {
                color = 0xFFFFFF;
            } else {
                color = 0xFF000000;
            }
        }
        image->setPixel(j, i, color);
    }
}
```

我们构造了一个正确大小的新 `QImage` 并将其赋值给 *image*。然后，我们遍历 XOR 和 AND 数组中的每个像素，并将它们转换为 32 位 ARGB 颜色规范。AND 和 XOR 数组的使用如下所示，用于获取每个光标像素的颜色：

| AND | XOR | 结果 |
|---|---|---|
| 1 | 1 | 反色背景像素 |
| 1 | 0 | 透明像素 |
| 0 | 1 | 白色像素 |
| 0 | 0 | 黑色像素 |

黑色、白色和透明像素没有问题，但在不知道原始背景像素颜色的情况下，无法使用 ARGB 颜色规范获取反色像素。作为替代，我们使用了一种半透明的灰色（`0x7F7F7F7F`）。

```cpp
++currentImageNo;
if (currentImageNo == numImages) {
    state = AfterImage;
    return true;
}
```

一旦我们完成了图像的读取，更新 `currentImageNo`，如果达到了图像总数，则更新 `state`。此时，设备指针将位于文件的末尾。

```cpp
bool CursorHandler::jumpToImage() {
    QImage image;
    return read(&image);
}
```

`jumpNextImage()` 函数用于跳转图像。为了简单起见，我们直接调用 `read()` 并忽略生成的 `QImage`。更有效的实现将使用存储在 `.cur` 文件中的信息直接跳转到文件的偏移位置。

```cpp
void CursorHandler::readHeaderIfNecessary() const {
    if (state != BeforeHeader) {
        return;
    }

    quint16 reserved;
    quint16 type;
    quint16 count;

    QDataStream in(device());
    in.setOrder(QDataStream::LittleEndian);

    in >> reserved >> type >> count;
    in.skipRawData(1);

    if (in.status() != QDataStream::Ok || reserved != 0
    || count == 0) {
        enterErrorState();
        return;
    }
    state = BeforeImage;
    currentImageNo = 0;
    numImages = int(count);
}
```

```cpp
void CursorHandler::enterErrorState() const
{
  state = Error;
  currentImageNo = 0;
  numImages = 0;
}
```

```cpp
QBitArray CursorHandler::readBitmap(int width, int height, QDataStream &in) const
{
  QBitArray bitmap(width * height);
  quint32 word = 0;
  quint8 byte;
  for (int i = 0; i < height; ++i) {
    for (int j = 0; j < width; ++j) {
      if ((j % 32) == 0) {
        word = 0;
        for (int k = 0; k < 4; ++k) {
          in >> byte;
          word = (word << 8) | byte;
        }
      }
      bitmap.setBit((height - i - 1) * width + j,
        word & 0x80000000);
    }
  }
  return bitmap;
}
```

`readmap()` 函数用于读取光标的 AND 和 XOR 掩码。这些掩码有两个异常特征。首先，它们从下到上存储行，而不是常见的从上到下的方法。其次，数据的字节序似乎与 .cur 文件中其他所有地方相反。由于此，我们必须在 `setBit()` 调用中反转 y 坐标，并且按字节读取掩码值，通过位移和掩码来提取其正确值。

要构建该插件，我们必须使用一个与之前用于 Bronze 风格插件的 .pro 文件（第493 页）非常的文件：

```
TEMPLATE      = lib
CONFIG        += pluginhandler.h \
HEADERS       = cursorplugin.h
SOURCES       = cursorhandler.cpp \
               cursorplugin.cpp
DESTDIR       = $$[QT_INSTALL_PLUGINS]/imageformats
```

Windows 光标插件完成了。其他图像格式的插件将遵循相同的模式，尽管有些实现了更多的 `QImageIOHandler` API，特别是用于写入图像的函数。其他类型的插件遵循这种模式，即拥有一个或多个提供底层功能的处理程序的插件包装器。

