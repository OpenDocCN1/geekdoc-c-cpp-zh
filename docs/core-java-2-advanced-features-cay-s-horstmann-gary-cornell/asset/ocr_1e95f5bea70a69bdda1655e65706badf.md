# ### 2.3.3 ZIP Archives

ZIP archives store one or more files in a (usually) compressed format. Each ZIP archive has a header with information such as the name of each file and the compression method that was used. In Java, you can use a `ZipInputStream` to read a ZIP archive. You need to look at the individual entries in the archive. The `getNextEntry` method returns an object of type `ZipEntry` that describes the entry. Pass the entry to the `getInputStream` method of the `ZipInputStream` to obtain an input stream for reading the entry. Then call `closeEntry` to read the next entry. Here is a typical code sequence to read through a ZIP file:

```
```java
ZipInputStream zin = new ZipInputStream(new FileInputStream(zipname));
ZipEntry entry;
while ((entry = zin.getNextEntry()) != null)
{
    InputStream in = zin.getInputStream(entry);
    read the contents of in
    zin.closeEntry();
}
zin.close();
```
```

To write a ZIP file, use a `ZipOutputStream`. For each entry that you want to place into the ZIP file, create a `ZipEntry` object. Pass the file name to the `ZipEntry` constructor; it sets the other parameters such as file date and decompression method. You can override these settings if you like. Then, call the `putNextEntry` method of the `ZipOutputStream` to begin writing a new file. Send the file data to the ZIP output stream. When you are done, call `closeEntry`. Repeat for all the files you want to store. Here is a code skeleton:

```
```java
FileOutputStream fout = new FileOutputStream("test.zip");
ZipOutputStream zout = new ZipOutputStream(fout);
for all files
{
    ZipEntry ze = new ZipEntry(filename);
    zout.putNextEntry(ze);
    send data to zout
    zout.closeEntry();
}
zout.close();
```
```

> > **NOTE:** JAR files (which were discussed in Volume I, Chapter 13) are simply ZIP files with a special entry—the so-called manifest. Use the `JarInputStream` and `JarOutputStream` classes to read and write the manifest entry.

ZIP input streams are a good example of the power of the stream abstraction. When you read data stored in compressed form, you don’t need to worry that