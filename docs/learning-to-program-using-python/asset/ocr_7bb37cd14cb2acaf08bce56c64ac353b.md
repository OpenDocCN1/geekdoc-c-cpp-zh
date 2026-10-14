# ## 10.1 File Operations

To keep things consistent, here's the list of Python file operations:

+   * `output = open(‘/tmp/spam’, ‘w’)` Create output file ('w' means write)
* `input = open(‘data’, ‘r’)` Create input file ('r' means read)
* `S = input.read()` Read entire file into a single string
* `S = input.read(N)` Read N number of bytes (1 or more)
* `S = input.readline()` Read next line (through end-line marker)
* `L = input.readlines()` Read entire file into list of line strings
* `output.write(S)` Write string S onto file
* `output.writelines(L)` Write all line strings in list L onto file
* `output.close()` Manual close (or it's done for you when automatically collected)

Because Python has a built-in garbage collector, you don't really need to manually close your files; once an object is no longer referenced within memory, the object's memory space is automatically reclaimed. This applies to all objects in Python, including files. However, it's recommended to manually close files in large systems; it won't hurt anything and it's good to get into the habit in case you ever have to work in a language that doesn't have garbage collection.

# ## 10.2 Files and Streams

Coming from a Unix-background, Python treats files as a data stream, i.e. each file is read and stored as a sequential flow of bytes. Each file has an end-of-file (EOF) marker denoting when the last byte of data has been read from it. This is useful because you can write a program that reads a file in pieces rather than loading the entire file into memory at one time. When the end-of-file marker is reached, your