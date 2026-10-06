from the given device. the canRead() function only peeks at the data, seeing
whether it recognizes the file, without changing the file pointer. A capability of 0\means that the file cannot be read or written by this handler.

```
QImageIOHandler CursorPlugin::create(QIODevice device,
            const QByteArray &format) const
{
    Cursor *handler = new CursorHandler;
    handler->setDevice(device);
    handler->setFormat(format);
    return handler;
}
```

When a cursor file is opened (e.g., by QImageReader), the plugin wrapper's
create() function will be called with the device pointer and with "cur" as the
. We create a CursorHandler instance and set it up with the specified
device and format. The caller takes ownership of the handler and will delete it
when it is no longer required. If multiple files are to be read, a fresh handler will be
created for each one.

```
Q_EXPORT_PLUGIN2(cursorplugin, CursorPlugin)
```

At the end of the .cpp file, we use the Q_EXPORT_PLUGIN2() macro to ensure that
Qt recognizes the plugin. The first parameter is an arbitrary name that we want to
give to the plugin. The second parameter is the plugin class name.
Subclassing QImageIOPlugin is straightforward. The real work of the plugin is
done in the handler. Image format handlers must subclass QImageIOHandler and
reinplement or all of its public functions. Let's start with the header:

```
class CursorHandler : public QImageIOHandler
{
public:
    CursorHandler();

    bool canRead() const;
    bool read(QImage *image);
    bool jumpToNextImage();
    int currentImageNumber() const;
    int imageCount() const;

private:
```