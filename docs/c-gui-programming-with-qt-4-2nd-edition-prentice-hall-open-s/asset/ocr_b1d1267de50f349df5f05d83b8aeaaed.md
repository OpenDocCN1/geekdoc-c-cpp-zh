```
textBrowser->setSearchPaths(QStringList() << path << \:/images\ntextBrowser->setSource(page);
```

We set the Qt::WA_GroupLeader attribute because we want to pop up HelpBrowser from modal dialogs in addition to the main window. Dialog normally prevent the user from interacting with any other window in the application. However, after requesting help, the user must obviously be allowed to interact with both the modal dialog and the help browser. Setting Qt::WA_GroupLeader attribute makes this interaction possible.

We provide two search paths, the first path in the file system that contains the application'sdocumentation, and the second path in the location of the image resources. The HTML can include references to images in the file system in the normal way and references to image resources using a path that begins with :/ (colon slash). the page parameter is the name of the documentation file, with an optional HTML anchor.

```
void HelpBrowser::updateWindowTitle()\{
  setWindowTitle(tr("Help: %1").arg(textBrowser->documentTitle()));
}
```

Whenever the source page changes, the updateWindowTitle() slot is called. The documentTitle() function returns the text specified in the page's <title> tag.

```
void HelpBrowser::showPage(const QString &page)
{
  QString path = directoryOf("doc").absolutePath();
  HelpBrowser *browser = new HelpBrowser(path, page);
  browser->resize(500, 400);
  browser->show();
}
```

In the showPage() static function, we create the HelpBrowser window and then show it. It will be destroyed automatically when the user closes it, and we set the Qt::WA_DeleteClose attribute in the HelpBrowser constructor. For this example, we assume that the documentation is located in the application's