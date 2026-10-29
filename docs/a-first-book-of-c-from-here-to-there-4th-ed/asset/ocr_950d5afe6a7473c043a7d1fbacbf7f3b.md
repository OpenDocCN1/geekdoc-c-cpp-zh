# Table 9.5 File Manipulation Methods (continued)

| Method Name | Description |
|---|---|
| getline(C-stringVar,int n,'\n') | Extract and return characters from the input stream until n-1 characters are read or a newline is encountered (terminates the input with a '\0'). |
| peek() | Return the next character in the input stream without extracting it from the stream. |
| put(chrExp) | Put the character specified by chrExp on the output stream. |
| putback(chrExp) | Push the character specified by chrExp back onto the input stream. Does not alter the data in the file. |
| ignore(int n) | Skip over the next n characters; if n is omitted, the default is to skip over the next single character. |
| eof() | Returns a Boolean true if a read has been attempted past the end of file; otherwise, it returns a Boolean false. The value becomes true only when the first character after the last valid file character is read. |
| good() | Returns a Boolean true while the file is available for program use. Returns a Boolean false if a read has been attempted past the end of file. The value becomes false only when the first character after the last valid file character is read. |
| bad() | Returns a Boolean true if a read has been attempted past the end of file; otherwise, it returns a false. The value becomes true only when the first character after the last valid file character is read. |
| fail() | Returns a Boolean true if the file hasn't been opened successfully; otherwise, it returns a Boolean false. |