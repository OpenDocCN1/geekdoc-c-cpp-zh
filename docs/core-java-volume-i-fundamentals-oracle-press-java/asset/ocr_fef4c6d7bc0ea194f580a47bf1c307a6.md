The manifest file is called `MANIFEST.MF` and is located in a special `META-INF` subdirectory of the JAR file. The minimum legal manifest is quite boring—just

```
```
Manifest-Version: 1.0
```
```

Complex manifests can have many more entries. The manifest entries are grouped into sections. The first section in the manifest is called the *main section*. It applies to the whole JAR file. Subsequent entries can specify properties of named entities such as individual files, packages, or URLs. Those entries must begin with a `Name` entry. Sections are separated by blank lines. For example:

```
```
Manifest-Version: 1.0
lines describing this archive

Name: Wozzle.class
lines describing this file
Name: com/mycompany/mypkg/
lines describing this package
```
```

To edit the manifest, place the lines that you want to add to the manifest into a text file. Then run

```
```
jar cfm jarFileName manifestFileName . . .
```
```

For example, to make a new JAR file with a manifest, run

```
```
jar cfm MyArchive.jar manifest.mf com/mycompany/mypkg/*.class
```
```

To update the manifest of an existing JAR file, place the additions into a text file and use a command such as

```
```
jar ufm MyArchive.jar manifest-additions.mf
```
```