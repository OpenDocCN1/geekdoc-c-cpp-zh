
Now for the random access group. Within `Windows.Storage.Streams` we find the basic types: `FileRandomAccessStream`, `InMemoryRandomAccessStream`, and `RandomAccessStream`, along with the abstract interface `IRandomAccessStream`. (`RandomAccessStreamOverStream` again builds on the low-level COM `IStream` and isn't something you use directly.)

The methods of `IRandomAccessStream` are common among classes in this group. It provides:

- Properties: `canRead`, `canWrite`, `position`, and `size`.
- Methods: `seek`, `cloneStream` (the clone has an independent position and lifetime), `getInputStreamAt` (returns an `IInputStream`), and `getOutputStreamAt` (returns an `IOutputStream`).

The `getInputStreamAt` and `getOutputStreamAt` methods are how you obtain a sequential stream for some section of the random access stream, allowing more efficient read/write operations. You often use these methods to obtain a sequential stream for some other API that requires them.

If we now look at `FileRandomAccessStream` and `InMemoryRandomAccessStream` (whose backing data sources I trust are obvious), they have everything we've seen already (properties like `position` and `canRead`, and methods like `close` and `seek`) along with two more methods, `readAsync` and `writeAsync`, that behave just like their counterparts in sequential input and output streams (using those buffers again).

As for the `RandomAccessStream` class, it's a curious beast that contains only static members—you never have an instance of this one. It exists to provide the generic helper methods `copyAsync` (with two variants) and `copyAndCloseAsync` that transfer data between input and output streams. This way other classes like `FileRandomAccessStream` don't need their own copy methods. To copy content from one file into another, then, you call `FileRandomAccessStream.getInputStreamAt` on the source (for reading) and `FileRandomAccessStream.getOutputStreamAt` on the destination (for writing), then pass those to `RandomAccessStream.copyAsync` (to leave those streams open) or `copyAndCloseAsync` (to automatically do a `flushAsync` on the destination and close both).

The other class to talk about here, `RandomAccessStreamReference`, also supplies other static members. When you read 'reference,' avoid thinking about reference types or pointers or anything like that—it's more about having read-only access to resources that might not be writable, like something at the other end of a URI. Its three static methods are `createFromFile` (which takes a `StorageFile`), `createFromStream` (which takes an `IRandomAccessStream`), and `createFromUri` (which takes a `Windows.Foundation.Uri` that you construct with a string). What you then get back from each of these static methods is an instance of `RandomAccessStreamReference` (how's that for confusing?). That instance then has just one method, `openReadAsync`, whose result is an `IRandomAccessStreamWithContentType` (the same thing as an `IRandomAccessStream` with an extra string property `contentType` to identify its data format).

To sum up, then, remember the difference between sequential streams (input or output) and random access streams, and that streams are just ways to talk to the bits (or bytes) that exist in some backing entity like a file or memory. When a stream exists, its backing entity is "open" and typically locked (depending on access options) until the stream is closed or disposed.

## Question #3: So now what do I do with these buffer objects, when neither the `Buffer` class nor the `IBuffer` interface has any methods?

### Answer

I totally agree that this one stumped me for a while, which is one reason I’ve included this Q&A section in this book!

As in question #2, straightforward stream object methods like `readAsync` and `writeAsync` result in this odd duck called a `Buffer` instead of just giving us a byte array. The problem is, when you look at the reference docs for `Buffer` and `IBuffer`, all you see are two properties: `length` and `capacity`. “That’s all well and good,” you say (and I have!), “but how the heck do you get at the data itself?” After all, if you just opened a file and read its contents from an input stream into a buffer, that data exists somewhere, but this buffer thing is just a black box as far as you can see!

Indeed, looking at the `Buffer` itself it's hard to understand how one even gets created in the first place, because the object itself also lacks methods for storing data in the first place (the constructor takes only a `capacity` argument). This gets confusing when you need to provide a buffer to some API, like `ProximityDevice.PublishBinaryMessage` (for near-field communications): you need a buffer to call the function, but how do you create one?

To make things clear, first understand that a buffer is just an abstraction for an untyped byte array, and it exists because marshaling byte arrays between Windows and language-specific environments like JavaScript and C# is a tricky business. Having an abstract class makes such marshaling easier to work with in the API.

Next, when you are about to call `FileRandomAccessStream.readAsync`, you do, in fact, create an empty buffer with `new Buffer()`, which `readAsync` will populate. On the other hand, if you need to create a new buffer with real data, there are two ways to go about it:

- One way is our friend `Windows.Storage.Streams.DataWriter`. Create an instance with `new DataWriter()`, then use its `write*` methods to populate it with whatever you want (including `writeBytes`, which takes an array). Once you’ve written those contents, call its `detachBuffer` and you have your populated `Buffer` object.
- The other way is super-secret, or maybe just unintentional but nonetheless useful here. You have to look way down in `Windows.Security.Cryptography`—wait for it—`CryptographicBuffer.createFromByteArray`. This API has nothing to do with cryptography per se and simply creates a new buffer with a byte array you provide. This is simpler than using `DataWriter` if you have a byte array; `DataWriter` is better, though, if you have data in any other form, such as a string.

How, then, do you get data out of a buffer? With the `Windows.Storage.Streams.DataReader` class. Create an instance of `DataReader` with the `static` method `DataReader.fromBuffer`, after which you can call methods like `readBytes`, `readString`, and so forth.⁸¹

In short, the methods that you would normally expect to find on a class like `Buffer` are found instead within `DataReader` and `DataWriter`, because these reader/writer classes also work with streams. That is, instead of having completely separate abstractions for streams and byte arrays with their own read/write methods for different data types, those methods are centralized within the `DataReader` and `DataWriter` objects that are themselves initialized with either a stream or a buffer. `DataReader` and `DataWriter` also take care of the details of closing streams for you when appropriate.

In the end, this reduces the overall API surface area once you understand how they relate.

## Question #4: Now doesn't all this business with streams and buffers make simple file I/O rather complicated?

### Answer

Yes and no, and for the most part we've already answered this question in the "FileIO, PathIO, and WinJS Helpers" section earlier with the RawFileWrite code examples. To reiterate, the low-level API gives you full control over the details; the higher-level APIs to simplify common scenarios.

Indeed, we can go even one step lower than our `writeTempFileRaw` function. In that code we used `DataWriter.storeAsync`, which is itself just a helper for the truly raw process that involves buffers. Here, then, is the lowest-level implementation for writing a file (see js/default.js in the example):

```javascript
var fileContents = "Congratulations, you're written data to a temp file!";
writeTempFileReallyRaw("data-raw.tmp", fileContents);

function writeTempFileReallyRaw(filename, contents) {
    var ws = Windows.Storage;
    var tempFolder = ws.ApplicationData.current.temporaryFolder;
    var writer;
    var outputStream;

    //All the control you want!
    tempFolder.createFileAsync(filename, ws.CreationCollisionOption.replaceExisting)
    .then(function (file) {
        //file is a StorageFile
        return file.openAsync(ws.FileAccessMode.readWrite);
    }).then(function (stream) {
        //Stream is a RandomAccessStream. To write to it, we need an IOutputStream
        outputStream = stream.getOutputStreamAt(0);
        //Create a buffer with contents
        writer = new ws.Streams.DataWriter(outputStream);
```

---

⁸¹ If you use `new` with `DataReader`, you provide an `IInputStream` argument instead—with buffers you have to use the `static` method. The reason for this is that JavaScript cannot differentiate overloaded methods by arity only (number of arguments), thus the designers of WinRT had to make a few oddball choices like this where the more common usage employs the constructor and a static method is used for the less common option.
