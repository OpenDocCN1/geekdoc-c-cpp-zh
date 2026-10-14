| Account | Name | Balance |
| :--- | :--- | :--- |
| 101 | Jeffrey | 100.50 |
| 105 | Patrick | 325.49 |
| 110 | Susan | 210.50 |

A shortcut would be rewriting the for block so it doesn't have to iterate through the variable individuals but to simply read the file directly, as such:

```
for record in file:
```

This will iterate through the file, read each line, and assign it to “record”. This results in each line being processed immediately, rather than having to wait for the entire file to be read into memory. The readlines() method requires the file to be placed in memory before it can be processed; for large files, this can result in a performance hit.

# 10.6 Seeking

Seeking is the process of moving a pointer within a file to an arbitrary position. This allows you to get data from anywhere within the file without having to start at the beginning every time.

The seek() method can take several arguments. The first argument (offset) is starting position of the pointer. The second, optional argument is the seek direction from where the offset starts. 0 is the default value and indicates an offset relative to the beginning of the file, 1 is relative to the current position within the file, and 2 is relative to the end of the file.

```
Listing 10.6: File seeking
file.seek(15) #move pointer 15 bytes from
beginning of file
file.seek(12, 1) #move pointer 12 bytes from
current location
file.seek(-50, 2) #move pointer 50 bytes backwards
from end of file
file.seek(0, 2) #move pointer at end of file
```

The tell() method returns the current position of the pointer within the file. This can be useful for troubleshooting (to make sure