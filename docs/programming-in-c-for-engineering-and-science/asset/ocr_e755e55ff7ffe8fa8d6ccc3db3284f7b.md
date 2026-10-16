+   - Opening an `ifstream` to a file initializes the file stream with the contents of that file and the read position at the first character in the file stream.
+   - Opening an `ofstream` to a file initializes the file stream as empty (containing only the end-of-file mark) with the write position at the end-of-file mark. Any previous contents of the file are destroyed.
+   - If an `ofstream` to a file is opened using `ios::app`, the stream is initialized with the contents of that file with the write position at the end of the file.
+   - After skipping leading white space characters, the input operator (`>>`) will extract the first value following the read position in an `ifstream` and advance the read position to the first character after the input value. Numeric values are delimited by nonnumeric characters.
+   - The `getline()` function extracts the line of input beginning at the read position in an `ifstream` and stores the extracted characters in a `string` variable, stopping when it reaches a newline character. It leaves the read position at the first character beyond that newline. Intermixing calls to `getline()` and the input operator must be done with caution.
+   - The output operator (`<<`) inserts a value into an `ofstream` at the current write position and advances it to the point immediately following the value.
+   - A file stream should be disconnected from a file by a call to `close()` when input/output is finished.

# 11.3 ADDITIONAL STREAM FEATURES

We have looked at the basic file-stream operations of `open()`, `is_open()`, `<<`, `>>`, `getline()`, `eof()`, and `close()`, but there are many others. Of these, we discussed in earlier chapters: `get()` to read a character from a stream without skipping white space; `good()`, `bad()`, and `fail()` to check a stream’s status; `clear()` to reset a stream’s status bits; `ignore()` to skip characters; and the various stream manipulators. The following table lists some of the stream messages that can be sent to both `istream` and `ifstream` objects, or to both `ostream` and `ofstream` objects. But this is not an exhaustive list; the `iostream` and `fstream` libraries are extensive and this table indicates only a small part of their capabilities.

| Function Member | Description |
|---|---|
| `good()` | true if the `good` bit is set (1) else false |
| `fail()` | true if the `fail` bit is set (1) else false |
| `bad()` | true if the `bad` bit is set (1) else false |
| `eof()` | true if the `eof` bit is set (1) else false |
| `clear()` | Reset the `good` bit to 1, all other status bits to 0 |
| `setstate(sBit)` | Set the status bit `sBit` to 1, where `sBit` is one or more of `ios::badbit`, `ios::failbit`, `ios::eofbit` |
| `get(ch)` | Read the next character (including white space) into `ch` |