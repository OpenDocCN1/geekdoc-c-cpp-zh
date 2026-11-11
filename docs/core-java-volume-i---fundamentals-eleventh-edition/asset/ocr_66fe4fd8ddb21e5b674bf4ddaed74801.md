Complex manifests can have many more entries. The manifest entries are grouped into sections. The first section in the manifest is called the *main section*. It applies to the whole JAR file. Subsequent entries can specify properties of named entities such as individual files, packages, or URLs. Those entries must begin with a `Name` entry. Sections are separated by blank lines. For example:

```
```
Manifest-Version: 1.0
lines describing this archive

Name: Woozle.class
lines describing this file
Name: com/mycompany/mypkg/
lines describing this package
```
```

To edit the manifest, place the lines that you want to add to the manifest into a text file. Then run

```
```
jar cfm jarFile Name manifestFileName . . .
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

> > **NOTE:** See https://docs.oracle.com/javase/10/docs/specs/jar/jar.html for more information on the JAR and manifest file formats.

# ### 4.8.3 Executable JAR Files

You can use the `e` option of the `jar` command to specify the *entry point* of your program—the class that you would normally specify when invoking the `java` program launcher:

```
```
jar cve MyProgram.jar com.mycompany.mypkg.MainAppClass files to add
```
```

Alternatively, you can specify the *main class* of your program in the manifest, including a statement of the form

```
```
Main-Class: com.mycompany.mypkg.MainAppClass
```
```

Do not add a `.class` extension to the main class name.