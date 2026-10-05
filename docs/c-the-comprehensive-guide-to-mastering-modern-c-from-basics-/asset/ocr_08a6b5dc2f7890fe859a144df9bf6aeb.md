write or read position or to change the position. In Table 27.12, you will find an overview of the available methods.

| Method | Description |
| --- | --- |
| istream& seekg(strepos), istream& seekg(strepos, ios::seekdir) | Sets the read position to a specific position from the beginning of the file or relative to the optionally specified second argument |
| ostream tellg() | Returns the current read position |
| ostream& seekp(strepos), ostream& seekp(strepos, ios::seekdir) | Sets the write position to a specific position from the beginning of the file or relative to the optionally specified second argument |
| opos tellp() | Returns the current write position |

**Table 27.12** Methods for random access.

The possible values for the second argument of seekg() and seekp() (g stands for get and p for put) for the reference position of type ios::seekdir are as follows:

+   - ios::beg: position relative to the beginning of the file
- ios::cur: position relative to the current position in the file
- ios::end: position relative to the end of the file