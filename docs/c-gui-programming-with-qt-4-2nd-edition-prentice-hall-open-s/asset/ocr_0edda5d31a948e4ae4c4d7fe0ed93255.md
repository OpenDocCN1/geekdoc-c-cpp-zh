# Traversing Directories

The QDir class provides a platform-independent means of traversing directories and retrieving information about files. To see how QDir is used, we will write a small console application that calculates the space consumed by all the images in a particular directory and all its subdirectories at any depth.

The heart of the application is the imageSpace() function, which recursively computes the cumulative size of a given directory's images:

```
qlonglong imageSpace(const QString &path)
{
    QDir dir(path);
    qlonglong size = 0;

    QStringList filters;
    foreach (QByteArray format, QImageReader::supportedImageFormats())
        filters += ".*" + format;

    foreach (QString file, dir.entryList(filters, QDir::Files))
        size += QFileInfo(dir, file).size();

    foreach (QString subDir, dir.entryList(QDir::Dirs | QDir::NoDotAndDotDot))
        size += imageSpace(path + QDir::separator() + subDir);

    return size;
}
```

We begin creating a QDir object using the given path, which may be relative to the current directory or absolute. We pass the entryList() function two arguments. The first is a list of file names. These can contain '*' and '?' wildcard characters. In this example, we are filtering to include only file formats that QImage can read. The second argument specifies what kind of entries we want (normal files, directories, drives, etc.).

We iterate over them (excluding . and ..) and recursively call imageSpace() to ascertain their accumulated image sizes. To create each subdirectory's path, we combine the current directory's path with the subdirectory name, separating them with a slash. QDir treats '/' as a directory separator on all platforms, in addition to recognizing '\' on Windows.