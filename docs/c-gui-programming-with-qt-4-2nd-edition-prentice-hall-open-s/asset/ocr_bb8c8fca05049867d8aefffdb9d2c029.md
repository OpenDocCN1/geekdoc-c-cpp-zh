```
QDataStream out(&file);
out.setVersion(QDataStream::Qt_4_3);
out << quint32(0x12345678) << image << map;
```

If we cannot open the file, we inform the user and return. The qPrintable() returns a const char * for a QString (Another approach would have been to use QString::toCString(), which returns a std::string, for which <iostream> has a overload.)

If the file is opened successfully, we create a QDataStream and set its version number. The version number is an integer that influences the way Qt data types are represented (base C++ data types are always represented the same way). In Qt 4.3, the most comprehensive format is version 9. We can either hard-code the constant 9 or use QDataStream::Qt_4_3 symbolic name.

To ensure that the number 0x12345678 is written as an unsigned 32-bit integer on all platforms, we cast it to quint32, a data type that is guaranteed to be exactly 32 bits. To ensure interoperability, QDataStream standardizes on big-endian by default; this can be changed by calling setByteOrder().

We don't need to explicitly close the file, since this is done automatically when the QFile variable goes out of scope. We want to verify that the data has actually been written, we can call flush() and check its return value (true on success).

The code to read back the data mirrors the code we used to write it:

```
quint32 n;
Image image;
QMap<QString, QColor> map;
```

```
QFile file("facts.dat");
if (!file.open(QIODevice::ReadOnly)) {
    std::cerr << "Cannot open file for reading: "
              << qPrintable(file.errorString()) << std::endl;
    return;
}
```

```
QDataStream in(&file);
in.setVersion(QDataStream::Qt_4_3);
in >> n >> image >> map;
```