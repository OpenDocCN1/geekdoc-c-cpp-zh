# Table 9.3 fstream Methods

| Method Name | Description |
|---|---|
| get() | Returns the next character extracted from the input stream as an int. |
| get(charVar) | Overloaded version of get() that extracts the next character from the input stream and assigns it to the specified character variable, charVar. |
| getline(strObj, termChar) | Extracts characters from the specified input stream, strObj, until the terminating character, termChar, is encountered. Assigns the characters to the specified string class object, strObj. |
| peek() | Returns the next character in the input stream without extracting it from the stream. |
| ignore(int n) | Skips over the next n characters. If n is omitted, the default is to skip over the next single character. |

Program 9.5 shows how the prices.dat file created in Program 9.4 can be read. This program illustrates one way of detecting the EOF marker by using the good() method (see Table 9.2). Because this method returns a Boolean true value before the EOF marker has been read or passed over, it can be used to verify that the data read is valid file data. Only after the EOF marker has been read or passed over does this method return a Boolean false. Therefore, the notation while(infile.good()) used in Program 9.5 ensures that data is from the file before the EOF has been read.