Whether you choose to use reference counting or are forced to use it, expect to spend many hours debugging memory leaks and fixing random crashes. Windows, Java, Flash, and Unix all include garbage collection. It can be challenging to have to get used to managing memory without automation. On the iPhone, this is one of Objective-C’s weakest and least appealing features. Fortunately the Xcode development tools include a set of applications that simplify testing and make it easier to monitor and track memory leaks.

# Objects and conditionals

You can’t create objects within a conditional block and refer to them outside it. For example, in

```
if (condition) {
    createAnObject;
    doOtherStuff...
}
doStuffWithTheNewObject;
```

the compiler can’t be sure if the object will exist outside of the conditional. It assumes that it doesn’t, and reports an error.

# Cocoa file management

Cocoa includes a file selector object that loads and displays a standard OS X file list. Under the hood, file management is less conventional. Files aren’t saved but archived. Archiving automatically includes a conversion stage that transforms an object or collection in memory into bytes on disk. Loading a file invokes a de-archiver that reverses the process.

This may appear indirect, but it’s an example of Cocoa’s emphasis on abstraction. When you’re saving an image to disk, you always need to convert it to a standard graphic file format before writing it out. Cocoa makes it easy to do this; for example, it includes a JPEG archiver. You can also create your own archiving and de-archiving code for custom file formats.

# Cocoa archiving

Cocoa’s data objects include built-in archiving. For example, you can write a dictionary to disk with

```
[aDictionary writeToFile: aFilePathString atomically: YES];
```

This automatically archives the dictionary and writes it to a file in a format that can be read back with a corresponding

```
thatOldDictionary =
[NSDictionary dictionaryWithContentsOfFile: aFilePathString];
```

![](bbox=[0.104, 0.839, 0.174, 0.895])

# NOTE

The atomically parameter selects a two-stage write that attempts to write a complete file, and then renames it to the specified file name if the write succeeds. If the write fails, the file fragment is deleted. This guarantees that files on disk are always complete.