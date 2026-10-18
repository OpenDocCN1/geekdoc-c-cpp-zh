> NOTE: We have used an fstream object to open the file. Since an fstream object can handle both the input and output simultaneously, we have opened the file in ios::in | ios::out mode. After writing the file, we want to read the entire file and display its contents. Since the file pointer has already moved to the end of the file, we must bring it back to the start of the file. This is done by the statement
> 
> file.seekg(O);

# write() and read() Functions

The functions write() and read(), unlike the functions put() and get(), handle the data in binary form. This means that the values are stored in the disk file in the same format in which they are stored in the internal memory. Figure 11.9 shows how an int value 2594 is stored in the binary and character formats. An int takes two bytes to store its value in the binary form, irrespective of its size. But a 4 digit int will take four bytes to store it in the character form.

![](bbox=[0.126, 0.588, 0.869, 0.821])