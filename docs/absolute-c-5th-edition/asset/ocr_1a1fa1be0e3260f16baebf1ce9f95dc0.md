# Random Access to Files

The constraints of finding a position and replacing one portion of a file with data mean that most random-access I/O is done by reading or writing records (in the form of structs or classes). One record (an integral number of records) is read or written after each positioning of the pointer.

Each ifstream object has a member function named seekp that is used to position the put-pointer at the location where you wish to write ("put") data. The function seekp takes a single argument, which is the address of the first byte to be written next. The first byte in the file is numbered zero. For example, to position the pointer in the file connected to the rwStream at the 1000th byte, the invocation would be

```
rwStream.seekp(1000);
```

Of course, you need to know how many bytes a record requires. The sizeof operator is used to determine the number of bytes needed for an object of a class or struct. Additionally, sizeof can be applied to any type, object, or value. It returns the size of its argument in bytes. The operator sizeof is part of the core C++ language and requires no include directive or using directive. Some simple examples are:

```
sizeof(s) // where s is string = "Hello";
sizeof(10)
sizeof(double)
sizeof(MyStruct) // where MyStruct is a defined type
```

Each of these returns an integer the size of its argument in bytes.

To position the put-pointer at the 100th record of type MyStruct in a file containing nothing but records of type MyStruct, the invocation would be

```
rwStream.seekp(100*sizeof(MyStruct));
```

The member function seekg is used to position the get-pointer to indicate where reading ("getting") of the next byte will take place. It is completely analogous to seekp. With the setup you have shown, you can write to the file "stuff" and read from it using the ifstream rwStream with the member functions put and get. There is also a member function that can write multiple bytes and a member read that can read multiple bytes.

Theoretically, you now know enough to do random-access file I/O. In reality, this is just a taste of what is involved. This section was designed to let you know what it is all about in a general sort of way. If you intend to do any real programming of random-access file I/O, you should consult a more advanced and specialized book.

# 557