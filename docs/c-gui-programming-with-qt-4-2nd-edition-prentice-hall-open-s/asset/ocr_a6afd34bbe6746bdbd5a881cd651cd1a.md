```
if (!file->open(QIODevice::WriteOnly)) {
    std::cerr << "Warning: Cannot write file "
    << qPrintable(QDir::toNativeSeparators(file->fileName()))
    << ":" << qPrintable(file->errorString())
    << std::endl;
    return;
}

tp.get(urlInfo.name(), file);
openedFiles.append(file);
} else if (urlInfo.isDir() && !urlInfo.isSymLink()) {
    pendingDirs.append(currentDir + "/" + urlInfo.name());
}
```

The ftpInfo() slot urlInfo parameter provides detailed information about a remote file. If the file is a normal file (not a directory) and is readable, we call get() to download it. The QFile object used for downloading is allocated using new and a pointer is stored in the openedFiles list.

If the QUrlInfo holds the details of a remote directory that is not a symbolic link, we add this directory to the pendingDirs list. We skip symbolic links because they can easily lead to infinite recursion.

```
void Spider::ftpDone(bool error) {
    if (error) {
        std::cerr << "Error: " << qPrintable(ftp.errorString())
        << std::endl;
    } else {
        std::cout << "Downloaded " << qPrintable(currentDir) << " to "
        << qPrintable(QDir::toNativeSeparators(QDir(currentLocalDir).canonicalPath()));
    }

    qDeleteAll(openedFiles);
    openedFiles.clear();

    processNextDirectory();
}
```

The ftpDone() slot is called when all the FTP commands have finished or if an