# Random File Access

In Chapter 3 and the preceding section, you learned how to read data from and write data to a file. More specifically, you used fstream objects to read data from a file and ofstream objects to write data to a file. However, the files were read and/or written sequentially. Reading data from a file sequentially does not work very well for a variety of applications. For example, consider a program that processes customers’ data in a bank. Typically, there are thousands or even millions of customers in a bank. Suppose we want to access a customer’s data from the file that contains such data, say, for an account update. If the data is accessed sequentially, starting from the first position and read until the desired customer’s data is found, this process might be extremely time consuming. Similarly, in an airline’s reservation system to access a passenger’s reservation information sequentially, this might also be very time consuming. In such cases, the data retrieval must be efficient. A convenient way to do this is to be able to read the data randomly from a file, that is, randomly access any record in the file.

In the preceding section, you learned how to use the stream function `read` to read a specific number of bytes, and the function `write` to write a specific number of bytes.

The stream function `seekg` is used to move the read position to any byte in the file. The general syntax to use the function seekg is:

```
```cpp
fileVariableName.seekg(offset, position);
```
```

The stream function `seekp` is used to move the write position to any byte in the file. The general syntax to use the function seekp is:

```
```cpp
fileVariableName.seekp(offset, position);
```
```

The offset specifies the number of bytes the reading/writing positions are to be moved, and position specifies where to begin the offset. The offset can be calculated from the beginning of the file, end of the file, or the current position in the file. Moreover, offset is a long integer representation of an offset. Table E-3 shows the values that can be used for position.

**TABLE E-3**  Values of position

| position | Description |
|---|---|
| `ios::beg` | The offset is calculated from the beginning of the file. |
| `ios::cur` | The offset is calculated from the current position of the reading marker in the file. |
| `ios::end` | The offset is calculated from the end of the file. |