
第二个方法处理数据+类型信息，就像 HTTP 响应需要将内容类型前置到数据流时那样。

-   openSequentialReadAsync 提供一个只读的 Windows.Storage.Streams.IInputStream 对象，通过它你可以按字节块读取文件内容，但无法跳回先前位置。当你只需要消费（读取）该流时，应始终使用此方法，因为它比随机访问流性能更好（源可以针对顺序读取进行优化）。
-   openTransactedWriteAsync 提供一个 Windows.Storage.StorageStreamTransaction，它基本上是一个围绕 IRandomAccessStream 的辅助对象，带有 commitAsync 和 close 方法来处理事务。在保存复杂数据时，这是必要的，以确保整个写入操作原子地发生，并且即使中断也不会导致文件损坏。文件访问示例的场景 5 展示了这一点。

StorageFile 类还提供静态方法 createStreamedFileAsync、createStreamedFileFromUriAsync、replaceWithStreamedFileAsync 和 replaceWithStreamedFileFromUriAsync。这些方法提供一个 StorageFile，你通常会通过合约将其传递给其他应用，我们将在第 15 章“合约”中进一步看到。这些方法的用处在于，在首次从底层文件请求数据之前（如果确实会发生这种请求），根本不会访问底层文件。

现在把这一切整合起来：下面是一段代码，使用我们目前看到的原始 API，在临时 AppData 文件夹中创建并打开一个“data.tmp”文件，并向其中写入给定字符串。这段代码位于本章的 RawFileWrite 示例中。我要明确说明，这里展示的内容利用了 WinRT 中的低级 API，并不是你通常使用的方式，我们将在下一节看到。尽管如此，它仍有启发意义，因为你偶尔可能需要对过程进行精确控制：

```
    var fileContents = "Congratulations, you're written data to a temp file!";
    writeTempFileRaw("data.tmp", fileContents);

    function writeTempFileRaw(filename, contents) {
        var ws = Windows.Storage;
        var tempFolder = ws.ApplicationData.current.temporaryFolder;
        var outputStream;

        //Promise chains, anyone?
        tempFolder.createFileAsync(filename, ws.CreationCollisionOption.replaceExisting)
        .then(function (file) {
            return file.openAsync(ws.FileAccessMode.readWrite);
        }).then(function (stream) {
            outputStream = stream.getOutputStreamAt(0);
            var writer = new ws.Streams.DataWriter(outputStream);
            writer.writeString(contents);
            return writer.storeAsync();
        }).done(/* Completed handler if necessary */);
    }
```

幸好我们不久前学习了链式异步操作！从 ApplicationData 对象获取一个 StorageFolder 开始，我们调用它的 createFileAsync 来获取一个 StorageFile。然后打开该文件以获得随机访问流。此时文件已打开并锁定，因此其他应用无法访问它。

现在，随机访问流本身没有任何读取或写入数据的方法。为此，我们使用 Windows.Storage.Streams 中的 DataReader 和 DataWriter 类。DataReader 接收一个 IInputStream 对象，该对象可通过 IRandomAccessStream.getInputStreamAt(<offset>) 获得。如这里所示，DataWriter 接收一个 IOutputStream，它同样可通过 IRandomAccessStream.getOutputStreamAt(<offset>) 获得。

然后，DataReader 和 DataWriter 类提供许多方法，可以按字符串（如上面的 writeString 所示）、按二进制或按特定数据类型读取或写入数据。使用 DataWriter 时，我们必须以调用其 storeAsync 来结束该过程，该方法会将数据提交到后备存储。对于 DataReader 和 DataWriter，丢弃对象将关闭文件并使流失效（请参见下面的“提示”）。

**注意** 如果使用事务性输出流，还需要在 DataWriter.storeAsync 之后的链中调用其 flushAsync 方法。

现在你可能会说：“你在开玩笑吧！只是为了向文件写入一个简单字符串，就要进行四个链式异步操作！这个 API 是谁设计的？”确实，当我们在 Microsoft 内部开始构建最初的 Store 应用时，这就是我们拥有的全部，我们也问过自己这些问题！毕竟，执行一些基本的文件 I/O 通常是你添加到 Hello World 应用中的第一件事，而这绝不简单。更糟的是，当时 JavaScript 中还没有用于异步操作的 Promise，因此我们不得不用原始嵌套操作来编写整个过程。那个年代就是这样。

幸运的是，更简单的 API 已经可用，而且不久之后又出现了更多。这些就是你在处理文件时通常会使用的 API，我们将在下一节看到。尽管如此，理解上面低级代码的结构仍然很重要，因为 DataReader 和 DataWriter 类是处理各种不同 I/O 流的重要机制，并且对数据编码过程至关重要。能够控制细节也支持这样的场景：应用中的不同组件都共同参与文件结构。因此，最好查看 DataReader/DataWriter 参考文档以及“读取和写入数据”示例，以熟悉这些功能。

**提示** 在 RawFileWrite 示例中，你不会看到对文件或流上的 close 方法的任何引用，因为 DataWriter 会自动处理这一点（DataReader 也会这样做）。事实上，流确实有一个 close 方法，它会关闭其后备文件，这正是 DataReader 和 DataWriter 对象在释放时调用的方法。但是，如果你通过这些对象的 detachStream 方法将流与它们分离，就必须自行调用流的 close。

在开发写入文件的应用时，如果看到指示文件仍处于打开状态的错误，请检查是否已正确关闭涉及的流。有关更多信息，请参见本章稍后的“关于文件、流、缓冲区和 Blob 的问答”。

## FileIO、PathIO 和 WinJS 辅助工具（以及 FileReader）

就文件 I/O 而言，简单是件好事，WinRT 的设计者确保最常见的场景不需要像上一节看到的那样冗长的异步操作链。`Windows.Storage.FileIO` 和 `PathIO` 类提供了这样一种精简接口——而且无需与流打交道！两者唯一的区别是，`FileIO` 方法接收 `StorageFile` 参数，而 `PathIO` 方法接收路径名字符串，后者假定你已经以编程方式访问该路径。除此之外，两个类都提供相同的方法：`read | write|BufferAsync`（这些方法处理字节数组）、`append | read | write|LinesAsync`（这些方法处理字符串数组）和 `append | read | write|TextAsync`（这些方法处理单个字符串）。对于字符串，`WinJS.Application` 为你的 AppData 文件夹进一步简化了事情：它的 `local`、`roaming` 和 `temp` 属性实现了一个名为 `IOHelper` 的接口，并提供 `readText` 和 `writeText` 方法，使你甚至无需接触 `StorageFile` 对象。

使用 `FileIO` 类，上一节中的代码可以简化为以下内容，这也可以在 RawFileWrite 示例（js/default.js）中找到：

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

下面是使用 `WinJS.Application.temp.writeText` 编写的相同内容，它是一个异步调用，如果需要，会返回一个 Promise：

```
WinJS.Application.temp.writeText(filename, fileContents);
```

更多示例可在[文件访问示例](#)的场景 3 中找到。你还有另一个选项——前提是文件已存在——使用 `PathIO.writeTextAsync` 方法和 `ms-appdata` URI，如下所示：

```
Windows.Storage.PathIO.writeTextAsync("ms-appdata:///temp/" + filename, contents);
```

通过异步 `readText` 方法从文件读取文本同样简单，并且 WinJS 通过 `IOHelper` 提供了另外两个方法：`exists` 和 `remove`。话虽如此，这些 WinJS 辅助工具仅适用于你的 AppData 文件夹，而不适用于更广泛的文件系统。对于应用之外的区域

⁸⁰ 如果你好奇为什么像 `readText` 和 `writeText` 这样的异步方法名称中没有 Async，这是 WinJS 设计者有意的选择，以遵循现有的 JavaScript 约定，即通常不使用这样的后缀。另一方面，WinRT API 与语言无关，因此有自己的 Async 后缀约定。
