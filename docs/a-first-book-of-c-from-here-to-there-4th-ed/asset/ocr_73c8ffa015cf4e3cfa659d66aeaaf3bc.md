Program 9.5 produces the following display:

```
Mats 39.95
Bulbs 3.22
Fuses 1.08
```

Examine the expression inFile.good() used in the while statement. This expression is true as long as the EOF marker hasn’t been read. Therefore, as long as the last character read is good (that is, the EOF marker hasn’t been passed), the loop continues to read the file. Inside the loop, the items just read are displayed, and then a new string and a double-precision number are input to the program. When the EOF has been detected, the expression returns a Boolean value of false and the loop terminates. This termination ensures that data is read and displayed up to, but not including, the EOF marker.

A replacement for the expression while(inFile.good()) is the expression while(!inFile.eof()), which is read as "while the end of file has not been reached." This replacement works because the eof() method returns a true only after the EOF marker has been read or passed over. In effect, the relational expression checks that the EOF hasn’t been read—hence, the use of the NOT operator, !.

Another means of detecting the EOF is to use the fact that the extraction operator, >>, returns a Boolean value of true if data is extracted from a stream; otherwise, it returns a Boolean false value. Using this return value, the following code can be used in Program 9.5 to read the file:

```
// read and display the file's contents
while (inFile >> descrip >> price) // check next character
cout << descrip << ' ' << price << endl;
```

Although this code seems a bit cryptic at first glance, it makes perfect sense when you understand that the expression being tested extracts data from the file and returns a Boolean value to indicate whether the extraction was successful.

Finally, in the previous while statement or in Program 9.5, the expression inFile >> descrip >> price can be replaced by a getline() method (see Table 9.3). For file input, this method has the following syntax:
getline(fileObject, strObj, terminatingChar)
fileObject is the name of the ifstream file, strObj is a string class object, and terminatingChar is an optional character constant or variable specifying the terminating character. If this optional third argument is omitted, the default terminating character is the newline ('\n') character. Program 9.6 shows using getline() in the context of a complete program.