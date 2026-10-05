# Flags for Opening a File

| Flag | Short | Description |
| --- | --- | --- |
| ios::in | Input | Open for reading (default for ifstream) |
| ios::out | Output | Open for writing (default for ofstream) |
| ios::app | Append | Always add something at the end when writing |
| ios::trunc | Truncate | The file length is set to 0, and existing content is deleted |
| ios::ate | At end | Positions the read or write position at the end of the file immediately after opening. Without this flag, the read and/or write position is usually at the beginning of the file after opening |