# FileIO, PathIO, and WinJS Helpers (plus FileReader)

Simplicity is a good thing where file I/O is concerned, and the designers of WinRT made sure that the most common scenarios didn’t require a long chain of async operations like we saw in the previous section. The `Windows.Storage.FileIO` and `PathIO` classes provide such a streamlined interface—and without having to muck with streams! The only difference between the two is that the `FileIO` methods take a `StorageFile` parameter whereas the `PathIO` methods take a pathname string, the latter assuming that you already have programmatic access to that path. Beyond that, both classes offer the same methods called `read | write|BufferAsync` (these work with byte arrays), `append | read | write|LinesAsync` (these work with arrays of strings), and `append | read | write|TextAsync` (these work with singular strings). With strings, `WinJS.Application` simplifies matters even further for your appdata folders: its `local`, `roaming`, and `temp` properties, which implement an interface called `IOHelper`, provide `readText` and `writeText` methods that relieve you from even having to touch a `StorageFile` object.

Using the `FileIO` class, the code in the previous section can be reduced to the following, which can also be found in the RawFileWrite example (js/default.js):

```
function writeTempFileSimple(filename, contents) {
    var ws = Windows.Storage;
    var tempFolder = ws.ApplicationData.current.temporaryFolder;

    tempFolder.createFileAsync(filename, ws.CreationCollisionOption.replaceExisting)
      .then(function (file) {
          ws.FileIO.writeTextAsync(file, contents);
      });
}
```

And here’s the same thing written with `WinJS.Application.temp.writeText`, which is an async call and returns a promise if you need it:

```
WinJS.Application.temp.writeText(filename, fileContents);
```

Additional examples can be found in Scenario 3 of the [File access sample](#). One other option you have—provided the file already exists—is using the `PathIO.writeTextAsync` method with an `ms-appdata` URI like so:

```
Windows.Storage.PathIO.writeTextAsync("ms-appdata:///temp/" + filename, contents);
```

Reading text from a file through the async `readText` method is equally simple, and WinJS provides two other methods through `IOHelper`: `exists` and `remove`. That said, these WinJS helpers are available for only your AppData folders and not for the file system more broadly. For areas outside app

⁸⁰ If you’re curious as to why async methods like `readText` and `writeText` don’t have Async in their names, this was a conscious choice on the part of the WinJS designers to follow existing JavaScript conventions where such a suffix isn’t typically used. The WinRT API, on the other hand, is language-independent and thus has its own convention with the Async suffix.