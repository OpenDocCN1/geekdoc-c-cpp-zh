**Table 4.2** jar Program Options

| Option | Description |
|---|---|
| `c` | Creates a new or empty archive and adds files to it. If any of the specified file names are directories, the jar program processes them recursively. |
| `C` | Temporarily changes the directory. For example,<br><br>```<br>jar cvf jarFileName.jar -C classes *.class<br>```<br>changes to the classes subdirectory to add class files. |
| `e` | Creates an entry point in the manifest (see Section 4.8.3). |
| `f` | Specifies the JAR file name as the second command-line argument. If this parameter is missing, jar will write the result to standard output (when creating a JAR file) or read it from standard input (when extracting or tabulating a JAR file). |
| `i` | Creates an index file (for speeding up lookups in a large archive). |
| `m` | Adds a manifest to the JAR file. A manifest is a description of the archive contents and origin. Every archive has a default manifest, but you can supply your own if you want to authenticate the contents of the archive. |
| `M` | Does not create a manifest file for the entries. |
| `t` | Displays the table of contents. |
| `u` | Updates an existing JAR file. |
| `v` | Generates verbose output. |
| `x` | Extracts files. If you supply one or more file names, only those files are extracted. Otherwise, all files are extracted. |
| `0` | Stores without ZIP compression. |

# 4.8.2 The Manifest

In addition to class files, images, and other resources, each JAR file contains a manifest file that describes special features of the archive.

The manifest file is called MANIFEST.MF and is located in a special META-INF sub-directory of the JAR file. The minimum legal manifest is quite boring—just

```
Manifest-Version: 1.0
```