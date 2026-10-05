# 196 Object-Oriented Programming with C++

```
//to the right from the its
//current position in the file
//take the put pointer to the end
//of the file (past the
//last byte)
```
ofile.seekp(0,ios::end);
```

```
ofile.seekp(-1,ios::end);
//take the put pointer to the last
//byte of the file
```

Let now understand the difference between ios::app and ios::ate flags. Both of these opens the file for appending and making the put pointer point at the end of the file by default (past the last existing byte). Neither of the two overflows an existing file. The difference between the two is that while the file ios::ate allows you to rewind the put pointer and modify the existing contents of the file, the file ios::app does not allow. In other words, if the file is using ios::app flag, an attempt to use the seekp() function for rewinding the put pointer will fail. The put pointer would continue to point at the end of the file. As bytes are appended to the file, the put pointer, as already mentioned, moves forward. Therefore, it cannot be rewound if the file is using the ios::app flag. In case of ios::ate, the put pointer can be rewound.

# 7.9.2 tellp() Function

The tellp() returns the current position of the put pointer. It has been defined in the class ostream

```
ostream::tellp();
```

In the following example, the current position of the put pointer is determined and stored in a program variable.

```
long pos = ofile.tellp(); //ofile is an object of the
//class ostream
```

# 7.9.3 seekg() Function

This function is used to explicitly make the get pointer point at a desired position in the open file. It is important to note that by default the get pointer points at the beginning of the file that is for reading. Every read operation pushes forward the get pointer by the number of bytes.
Theseekg() function has been defined in the class istream. It has two versions.

```
istream & istream :: seekg(streamspos pos);
istream & istream :: seekg(streamoff off,
ios::seek_dir dir);
```

The explanation for these two versions of the seekg() function is similar to the one provided for the corresponding versions of seekp() function.

# 7.9.4 tellg() Function

The tellg() function, like the tellp() function, returns the current position of the get pointer. It has been defined in the class istream.

```
istream::tellg();
```