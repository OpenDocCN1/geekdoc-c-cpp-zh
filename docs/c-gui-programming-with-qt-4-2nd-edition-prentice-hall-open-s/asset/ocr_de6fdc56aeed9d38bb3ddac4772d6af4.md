```
enterErrorState();
return;
}
  state = BeforeImage;
  currentImageNo = 0;
  numImages = int(count);

```

The readHeaderIfNecessary() private function is called from imageCount() and read(). If the file's header has already been read, the state is not BeforeHeader and we return immediately. Otherwise, we open a stream on the device, read in some generic data (including the number of cursors in the file), and set the state to BeforeImage. At the end, the device's file pointer is positioned before the first image.

```
void CursorHandler::enterErrorState() const
{
  state = Error;
  currentImageNo = 0;
  numImages = 0;
}
```

If an error occurs, we assume that there are no valid images and set the state to Error. Once in the Error state, the handler's state cannot change.

Code View:

```
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
    }
  }
}
```