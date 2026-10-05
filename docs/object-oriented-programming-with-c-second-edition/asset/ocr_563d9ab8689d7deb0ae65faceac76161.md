# Stream and File Handling 177

memory, which is four. Thus, if a number of values are output in binary mode, the size of the output file will always be a multiple of four. Obviously, we can determine the size of the file and divide it by four to find the number of integers (records) that are stored in the file.

We can apply this simple technique to values of other types including objects. Suppose an object consists of an integer (four bytes), a float (four bytes), and a double (eight bytes). This object occupies 16 bytes in the memory. If output in binary mode, it will occupy 16 bytes in the output file.

The C++ standard library provides functions that input (read from files and write the values into) binary mode. These functions require the address of the value whose data needs to be input along with size. The code inside these functions reads the value from a point in the input file at which a temporary pointer points (more about this pointer later). The size of the block of bytes this code reads is equal to the supplied size. The code writes the data into the memory block where starting is equal to the supplied address. Functions that output in binary mode work in a similar fashion. As we see, binary functions treat size as the delimiter while reading data from disk. Therefore, the functions that write data into the disks need not insert an artificial delimiter when the data is output.

Let us contrast this what happens in text mode. Records stored in the output file are of variable length. Again, for our understanding, let us take the case of an integer-type variable. Its value is always stored in '1' a disk file in text mode. If its value is '1', it will occupy one byte in the file although it occupies four bytes in the memory. If its value is '11', it will occupy two bytes in the output file although it occupies four bytes in the memory. If its value is '111', it will occupy three bytes in the output file although it occupies four bytes and so on.

Thus, in case values are output in text mode, size of the output value is not fixed. Hence, size cannot be used as the delimiter by functions that will read the output values in future. But, for this code, the that calls a text mode function for output should also insert a delimiter of choice in the output file after every such call. This ensures that any piece of code is able to successfully read this output value.

Choosing a suitable delimiter is certainly an issue. There should be no chance of the delimiter itself becoming a part of the output value anytime in the future. But this is difficult to guarantee.

There is another difference in outputting in text mode. The size of a file does not indicate the number of records stored in it. This is because the size of the records is not fixed.

# 7.5 Text Output/Input

# 7.5.1 Text Output

Text output is achieved in C++ by:

+   * The insertion operator
* The put() function