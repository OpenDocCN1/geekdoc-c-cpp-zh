backing entity like a file or memory. When a stream exists, its backing entity is "open" and typically locked (depending on access options) until the stream is closed or disposed.

**Question #3:** So now what do I do with these buffer objects, when neither the `Buffer` class nor the `IBuffer` interface has any methods?

**Answer:** I totally agree that this one stumped me for a while, which is one reason I’ve included this Q&A section in this book!

As in question #2, straightforward stream object methods like `readAsync` and `writeAsync` result in this odd duck called a `Buffer` instead of just giving us a byte array. The problem is, when you look at the reference docs for `Buffer` and `IBuffer`, all you see are two properties: `length` and `capacity`. “That’s all well and good,” you say (and I have!), “but how the heck do you get at the data itself?” After all, if you just opened a file and read its contents from an input stream into a buffer, that data exists somewhere, but this buffer thing is just a black box as far as you can see!

Indeed, looking at the `Buffer` itself it’s hard to understand how one even gets created in the first place, because the object itself also lacks methods for storing data in the first place (the constructor takes only a `capacity` argument). This gets confusing when you need to provide a buffer to some API, like `ProximityDevice.PublishBinaryMessage` (for near-field communications): you need a buffer to call the function, but how do you create one?

To make things clear, first understand that a buffer is just an abstraction for an untyped byte array, and it exists because marshaling byte arrays between Windows and language-specific environments like JavaScript and C# is a tricky business. Having an abstract class makes such marshaling easier to work with in the API.

Next, when you are about to call `FileRandomAccessStream.readAsync`, you do, in fact, create an empty buffer with `new Buffer()`, which `readAsync` will populate. On the other hand, if you need to create a new buffer with real data, there are two ways to go about it:

+   - One way is our friend `Windows.Storage.Streams.DataWriter`. Create an instance with `new DataWriter()`, then use its `write*` methods to populate it with whatever you want (including `writeBytes`, which takes an array). Once you’ve written those contents, call its `detachBuffer` and you have your populated `Buffer` object.
+   - The other way is super-secret, or maybe just unintentional but nonetheless useful here. You have to look way down in `Windows.Security.Cryptography`—wait for it—`CryptographicBuffer.createFromByteArray`. This API has nothing to do with cryptography per se and simply creates a new buffer with a byte array you provide. This is simpler than using `DataWriter` if you have a byte array; `DataWriter` is better, though, if you have data in any other form, such as a string.