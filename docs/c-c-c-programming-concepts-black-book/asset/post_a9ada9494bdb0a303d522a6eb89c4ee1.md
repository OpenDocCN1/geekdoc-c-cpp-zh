
In the preceding example, we have examined the error state of a stream object to find out whether we have reached the end of file, as follows:

```cpp
while (infile)
{
    // ... Processing of File
}
```

In the preceding code snippet, infile becomes zero when end of file is reached.

The ios::nocreate flag reports an error when opening a file, if the file does not exist. The modified diskin() function is as follows:

```cpp
void Medicine_File::diskin(void)
{
    ifstream ifile("MEDICINE.TXT", ios::nocreate);
    if (ifile)
    {
        ifile.read((char *) &buffer, sizeof(buffer));
        while (ifile)
        {
            buffer.showdata();
            ifile.read((char *) &buffer, sizeof(buffer));
        }
    }
    else
    {
        cout<< "The file does not exist!";
    }
}
```

In case MEDICINE.TXT does not exist, the value of ifile will become zero and the error message “The file does not exist!” appears on the screen.

## The Stream Status Bits

The C++ I/O system maintains the status information about the outcome of each I/O operation. The state is indicated by the setting (0 or 1) of a set of bits, and these bits are defined by the io_state variable declared in the ios class. Table 15.2 lists the stream status bits:

**Table 15.2: Stream Status Bits**

| Status Bit | Description |
| --- | --- |
| eofbit | Set when an input stream is at its end. It indicates that no more characters are available for extraction. |
| failbit | Set when the last insertion or extraction has failed. This is a recoverable error. The stream is still in a usable state. |
| badbit | Set when an illegal insertion or extraction is attempted. The stream is not suitable for further use. Usually, it is set when opening a nonexistent file or seeking when a past EOF has occurred. |
| hardfail | Set when a hardware failure has occurred. The error that sets hardfail is usually unrecoverable. |

The following section explains the member functions for accessing stream status bits.

### Member Functions for Accessing Stream Status Bits

In this section, we will provide a list of member functions that are used for accessing stream status bits. Table 15.3 provides a list of the member functions and their description:

**Table 15.3: Member Functions**

| **Member Function** | **Description** |
| --- | --- |
| `int good()` | Returns a non-zero value if the stream is OK; otherwise, returns zero |
| `int bad()` | Returns a non-zero value if the badbit or hardfail bit is set; else, returns zero |
| `int eof()` | Returns a non-zero value if the eofbit is set; else, returns zero |
| `int fail()` | Returns a non-zero value if the failbit, badbit, or hardfail bit is set |
| `int rdstate()` | Returns the current value of the iostate variable |
| `void clear(int ef=0)` | Sets the error flags to ef; by default, ef equals zero, which resets all the error bits |

Next, let’s learn about random access.

## Random Access

The C++ I/O program manages two integer values for a file. One is the get pointer, which specifies where within the file the following input or read operation will happen. The other is the put pointer, which specifies where within the file the output or create operation will happen. These two pointers signify the present positions for the actual read and create, respectively. Each time an input or output operation happens, the pointers tend to be immediately advanced sequentially by the number of bytes read or even composed. The term pointers with this context must not be confused with the normal C++ pointers utilized as address parameters, but rather within the context with the present offset position originating from where an input or may be an output operation would be to happen. Usually, we may need to start reading a current file right from the start, and continue sequentially till the final outcome. When writing, we might want to start from the beginning, deleting any current contents or append through the end. These would be the default activities; therefore, no manipulations using the file pointers are crucial. However, there may be situations when we must manage the file pointers directly to help in reading from and writing to an arbitrary location within the particular file.

The `seekg()` and `tellg()` functions allow us to set and examine the get pointer; whereas, the `seekp()` and `tellp()` functions allow us to set and examine the put pointer. Therefore, we can access the file in a random access mode using these functions. All the objects of the iostream classes can be manipulated using either the seekg() function or the seekp() function. These functions move the get and put pointers to an absolute offset within the file, or a certain number of bytes relative to a certain position. The tellg() and tellp() functions can be used to find out the current position of either the get or put pointer in a file.

The seekg() function takes two arguments. The first argument could be a long integer specifying how many bytes (also called offset) to position the pointer. The second argument may be the reference point. For example, `file.seekg(10, ios::beg)` positions the pointer 10 bytes relative to the beginning of the file. The three reference points defined within this class are shown in Table 15.4:

**Table 15.4: Reference Points**

| **Reference Point** | **Description** |
| --- | --- |
| `ios::beg` | Denotes the beginning of the file |
| `ios::cur` | Denotes the current position of the file pointer |
| `ios::end` | Denotes the end of the file |

A negative value can also be specified for the first argument of the seekg() function. It helps in moving the file pointer backwards relative to the end of file. For example, the following statement moves the file pointer backwards by 20 bytes relative to the end of file:

```cpp
file.seekg(-20, ios::end);
```

If supplied with only one argument, ios::beg is assumed by default. For example, consider the following statement:

```cpp
file.seekg(16);
```

In the preceding statement, ios::beg will be the reference point by default. The tellg() function, on the other hand, does not have any arguments. It returns the existing byte position with the get pointer relative to the start of the file. Consider the following statement:

```cpp
long position = file.tellg();
```

This would result in the position variable taking the value of the current position of the get pointer. The seekp() and tellp() functions are identical in functionality to the seekg() and tellg() functions, except that they relate to the put pointer. The seekg() and tellg() functions are defined in the istream class and the seekp() and tellp() functions are defined in the ostream class.

### Example of Random Access

After we open a file in C++, we can place two file pointers – one for read and another for write – anywhere within the file including the end of file to read or write data from it. However, in random access, there is a complete freedom to read or write data from anywhere within the file. This section explains how we can query a file randomly to access information from it. Consider the following example to retrieve a particular record from the MEDICINE.TXT file:

```cpp
void main()
{
    medicine medobj;
    fstream ifile("MEDICINE.TXT",ios::in);
    ifile.seekg(0, ios::end);
    long endpos = ifile.tellg();
    cout<< "\n the size of the file is:" << endpos;
    cout<< "\n the size of a medicine record is:" << sizeof(medicine);
    int n = endpos/sizeof(medicine);
    cout<< "\n" << n << "medicine records exists in the file";
    cout<< "\nmedicine record query:";
    cout<< "\nwhich record do you want to query?";
    cout<< "\nPlease enter the record number";
    int num;
    cin>> num;
    int seekpos = (num - 1)*sizeof(medicine);
    ifile.seekg(seekpos);
    ifile.read((char *) &medobj, sizeof(medicine));
    medobj.showdata();
}
```

In the preceding example, querying will be based on the record number that a user wishes to query. If the user wishes to view the 15th record, then seekg(15*sizeof(medicine), ios::beg) would be enough to take us to the beginning of the 15th record.

## Formatted I/O – ios Format Functions

The C++ I/O system enables us to format I/O procedures. For example, we are able to set an area width, specify a number base, or figure out how many digits following the decimal point is going to be displayed. There are two related but conceptually different ways that we could use to format data. First, we can access the
