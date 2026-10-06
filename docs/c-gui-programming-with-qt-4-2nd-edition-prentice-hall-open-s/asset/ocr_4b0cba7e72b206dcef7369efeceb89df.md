Clipboard applications make use of Qt's built-in clipboard handling in one way or another. For example, the QText class uses cut(), copy(), and paste() as well as keyboard shortcuts, so little or no additional code is required.

When writing our classes, we can access the clipboard through `UIApplication::clipboard()`, which returns a pointer to the application's `QClipboard` object. Handling the system clipboard is easy: Call `setText()`, `setImage()`, or `setPixmap()` to put data onto the clipboard, and call `text()`, `image()`, or `pixmap()` to retrieve data from the clipboard. We have already seen examples of clipboard use in the Spreadsheet application from Chapter 4.

For some applications, the built-in functionality might not be sufficient. For example, we might want to provide data not just text or an image, or we might want to provide data in many different formats for maximum interoperability with other applications. The issue is very similar to what we encountered with drag and drop, and the answer is also similar: We can subclass `QMimeData` and reimplement a few virtual functions.

If our application supports drag and drop through a `QMimeData` subclass, we can simply reuse the `QMimeData` subclass and put it on the clipboard using the `setMimeData()` function. To retrieve the data, we can call `mimeData()` on the clipboard.

On X11, it is usually possible to paste a selection by clicking the middle button of a three-button mouse. This is done using a separate "selection" clipboard. If you want widgets to support this kind of clipboard as well as the standard, you must pass `QClipboard::Selection` as an additional argument to the various clipboard calls. For example, here's how we would implement `mouseReleaseEvent()` in a text editor to support pasting using the middle mouse button:

```
void MyTextEditor::mouseReleaseEvent(QMouseEvent event) {
    QClipboard clipboard = QApplication::clipboard();
    if (event->button() == Qt::MidButton
        && clipboard->supportsSelection()) {
        QString text = clipboard->text(QClipboard::Selection);
        pasteText(text);
    }
}
```

On X11, the `supportsSelection()` function returns `true`. On other platforms, it returns `false`.

If we want to be notified whenever the clipboard's contents change, we can