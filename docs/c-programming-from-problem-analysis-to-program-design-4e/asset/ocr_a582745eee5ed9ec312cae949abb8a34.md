Tables 13-5 and 13-6 show members of the StreamWriter and StreamReader classes.

# TABLE 13-5  StreamWriter members

| StreamWriter members | Description |
|---|---|
| `AutoFlush` | (Property) Gets or sets a value indicating whether the StreamWriter flushes its buffer to the underlying stream after calls to the `Write()` or `WriteLine()` methods |
| `Close()` | Closes the current StreamWriter |
| `Dispose()` | Releases the unmanaged resources used by the StreamWriter |
| `Flush()` | Clears all buffers for the current writer and causes any buffered data to be written to the underlying stream |
| `NewLine` | (Property) Gets or sets the line terminator string used by the current TextWriter |
| `Write()` | Writes the characters to the stream |
| `WriteLine()` | Writes the characters to the stream, followed by a line terminator |

# TABLE 13-6  StreamReader members

| StreamReader members | Description |
|---|---|
| `Close()` | Closes the current StreamReader |
| `DiscloseBufferedData()` | Allows the StreamReader to discard its current data |
| `Dispose()` | Releases the unmanaged resources used by the StreamReader |
| `Peek()` | Returns the next available character but does not consume it |
| `Read()` | Reads the next character or next set of characters from the input stream |

_(continues)_